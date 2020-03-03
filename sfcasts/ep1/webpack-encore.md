# Webpack Encore

Coming soon...

Our CSS and JavaScript set up is fine. We have a public directory of an app, CSS we
created. We have a question show dot JS and inside of our templates like base
.html.twig, we're just linking to the CSS files directly other than this asset
function, which really doesn't do anything. Symfony isn't touching our assets at all.
We're just doing things a very traditional way and that's fine. But if you want to be
very serious about front end development, um, in this day and age we need to take
this up to a next level. We need to use a node library called Webpack, which is an
absolute industry standard for sort of combining your CSS and JavaScript files and
creating a very robust front end system. Now what back can be a lot of work can be a
lot of work to set up. So in the Symfony world we use a wonderful library called
Webpack Encore to make this dead simple and we have an entire free tutorial on
Webpack Encore.

But I'm going to give you a quick view into how it works right now before we start.
Make sure you haven't node installed and also that you have yarn installed. Yarn is
one of the package managers for node, so it's kind of like composer for note. No,
it's all Encore. We're going to run the composer require Encore. Now I know a second
ago, Oh, before you do this, you should commit everything. I know a second ago I said
that Encore is a node library, so why are we installing it via composer? This is a
package library for PHP. What reality, all this does is installed a very small bundle
called Webpack Encore bundle, which helps integrate with Webpack Encore. The real
beauty of this, uh, of installing this library is that it brought in a fairly large
recipe which bootstrapped a whole bunch of stuff for us.

One cool thing is it modified our dot get ignore file. So if we go over here, I can
open the doc, get ignore file and you can see down here it added some new entries for
node modules. That's basically the vendor directory for node and a couple other paths
that we want to ignore and it boosts up a couple. It also added some Yammer files.
Don't worry about those. And bootstrapped a package. Dot JSON. This is the composer
dot JSON file for node and also a very important Webpack dot config dot JS file,
which makes this whole thing work. We're not going to look at those files and too
much detail. We'll save that for the full Encore tutorial. So check out there if you
want to.

Now that we have this package, that JSON file, which specifies our no dependencies,
we're gonna install them by saying yarn install. This is basically gonna read that
file and download a ton of files and directories into a new node_modules directory.
It might take a few moments to download everything and build a couple of packages.
When it's done. You'll see two new things inside of here. First you'll see a new node
modules director with tons of stuff in it. This is already being ignored from get,
which is good. And it also created a yarn dot lock file, which is just like the
composer to a lock file. So you'll also want to commit the yarn dot locked file.
Okay. So here's how this whole thing works. Close a couple of files, the recipe, edit
a new assets directory with a couple of examples, CSS and jobs in your files. There's
an app dot JS which just basically just console.log( something. And there's an app
that CSS, which just changes the background color to light to gray.

Webpack Encore is already configured to point at these files so it knows it needs to
process those files that happens thanks to this Webpack dot config, that J S file,
which we're not going to talk very much about, but this is where uh, how a web Encore
knows to look at that app dot JS file. So to execute Encore, find your terminal and
run yarn. Watch is actually a shortcut command for running an Encore executable dev
dash dash watch. Again more than that, noon in a different tutorial. The really
important thing here is that it parse through these two source files here and then
created a public build directory with a built version of app dot CSS and a built
version of app dot JS. And if we, and yes we can do a production build was Encore,
which would admit it by those. There's a lot more going on here, but that's basically
the idea. So now in our base template, instead of pointing directly at our public CSS
files, we can now point at this public and build stuff. There's an easy way to do
that. I'm going to remove my old link tag. We can say curly curly on port entry link
tags, and then just say app meaning because this is the name of these files is app.
And then down here on the bottom I'm going to say curly curly Encore entry script
tags app to get the same thing.

Now if we move over and refresh, did it work? It actually did see that gray
background there. It totally is loading those in. If I go to inspect here and look at
my console, you can see hello, Webpack Encore, edit me and assets, JS, app dot JS.
And just to show you in the uh, a view source here, there's nothing special going on
here. It's just rent the rendering, the build /link tag to build such app dot CSS. So
the cool thing is that now we can move our CSS into the CSS file. So I'm gonna copy
my public CSS app dot CSS. I'm gonna copy all of this. What was that file right click
go to refactor, delete. And then I'm going to go to app dot CSS and paste over this.

And as soon as I do that, if I refresh, it works. The reason is that if you look back
in your terminal, yarn watch is actually watching our files for changes so many times
we make, anytime we make any changes to those files, it automatically rebuilds the
files and public /bill. So we just let this run in the background. So let's do the
same thing for our JavaScript file. I'm going to open questions show dot JS and
instead of having a page specific JavaScript for simplicity, I'm just going to put
this right into my global app dot JS. So this'll be loaded on every page now. And
then I'm going to delete my JS directory entirely back. Let's delete our CSS
directory entirely.

And then I'm also going to go into templates. Questions showed at H month week, and
at the bottom we'll remove our page specific JavaScript here. And with any luck that
should have rebuilt my JavaScript. So if I click into his page here, I'm actually
gonna do a force refresh just to be totally sure. I'll close this. And yes, this
still works. Our app dot JS is being compiled down and the final public build app dot
JS now contains that coat. So the really cool thing is that now that you're in this
system, you can do, um, there's a couple of cool things that you can do. There's a
lot of cool things you can do. The most, the most important one is that instead of,
you know, using CDNs or downloading jQuery directly in your project, you can properly
install jQuery into your node dot modules directory. Then import it. So check this
out. I'm going to open a new terminal tab over here and say yarn, add jQuery dash
dash Def. This is the equivalent to composer require the dash dash dead part. There
is not actually important to you can use it or not use it. Now I'm going to go over
to my base template and remove jQuery entirely from my layout.

Go back and open my inspector here because if I refresh, our page is totally broken.
You can see dollar sign is not defined coming from our app dot JS file, so jQuery
does not exist right now. We did just download it into our node modules directory.
You would find a jQuery directly inside of here, but it does, but it's not being
included yet. The way to do that once you're inside Encore is via this handy import
statements, import dollar sign fromJ query because jQuery is the name of the library
installed. Now all these dollar signs here are referencing thatJ query variable
inside of there. When OnCourse, when mug Webpack Encore sees this, it's going to
automatically package jQuery into the final app dot JS file. Basically, it's a fancy
way of saying whenever I go over here and refresh, it just works. No heirs and jQuery
is now being properly brought in and packaged.

We can also do the same thing of bootstrap with a CSS. So up here you can see one of
the CSS I'm bringing in as bootstrap CSS. So I'm going to delete that. No surprise if
we refresh. Now that's going to make our page super duper ugly. So let's spin back
over here and run yarn add bootstrap dash dash dev. This is going to install
bootstrap, which is actually a collection of JavaScript and CSS files into our node
modules directory. And in this case we will want to bring in the bootstrap CSS. So
I'm gonna go into my app that CSS and check this out.

We can actually use the old act import syntax, double quotes. And then if you want to
reference a load, somebody from your node modules directory, the special syntax here
where you say till date bootstrap and that's it. It's going to know to bring in the
bootstrap CSS. So now I go over refresh doing anything else that reloads Webpack.
Encore is smart enough now to grab the bootstrap dot CSS and include that inside of
the final app dot CSS file. So that's just the tip of the artist's Berg with Webpack
Encore. But we now have a very nice robust system set up there. Webpack Encore can
also do production builds where it minimizes and combines files. Um, it supports sass
or less. You can, um, get it, uh, enable react or view support. Automatic versioning.
The sky is the limit. So if you're interested, go check out our free Webpack Encore
tutorial that's gonna make you an absolute expert on this, our friends. That's it for
this tutorial. I hope you're feeling really excited. We've already learned a lot of
Symfony and the next tutorial we're going to tackle, we're really going to dive into
Symfony and tackle that topic of services more and more because once you understand
services and how they work, you are going to be unstoppable inside of Symfony. Our
friends see you next time.
