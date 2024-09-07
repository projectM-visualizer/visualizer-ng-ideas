Building A Next-Generation Visualizer
=====================================

With this repository, the projectM team encourages the community to gather ideas, features and any other valuable input
we may use to build a new visualizer and preset format in the future.

As of now, we don't write any code or take PRs. First, we want to hear from :index_pointing_at_the_viewer: YOU what the
new visualizer should be capable of. This can be highly technical stuff, editing, scripting and rendering capabilities
or use-case specific features. Not everything will make it into the core visualizer, but we need to know how you would
use it, what you need to write awesome presets and on which platforms you see it running.

## How To Contribute

First, please read this file to the end to get an idea of what we're going to build and what the reasoning behind this
is. If you've done that already - great! Go start browsing the project wiki and discuss suggestions:

- [Use the wiki](https://github.com/projectM-visualizer/visualizer-ng-ideas/wiki) to collect suggestions and feature
  requests. Everyone with a GitHub account can edit the wiki.
- For everything that needs
  discussing, [use the discussions board instead](https://github.com/projectM-visualizer/visualizer-ng-ideas/discussions).

Please keep discussions out of the wiki. Be excellent to each other and keep all discussions and editing friendly and
professional. The projectM team will strictly moderate violations and remove and report offending content/users if
necessary.

## What Is the Goal And Why A New Visualizer?

There already are many music visualizers available. Some firmly integrated as part of a specific player, others are
standalone applications and some, like projectM, built as reusable libraries with an API to integrate into any
application.

Most of these visualizers aren't highly configurable or versatile, often just rendering a single or a few hard-coded
effects wich some random colors and movement applied. Only two have really taken off and created a whole community
around them creating stunning presets and effects, and both were original Winamp
plug-ins: [Milkdrop](https://en.wikipedia.org/wiki/MilkDrop) and the [Advanced
Visualization Studio](https://en.wikipedia.org/wiki/Advanced_Visualization_Studio). The former has definitely gained
more popularity, as the presets are easier to share and create,
while AVS is a bit more versatile as users could write their own effects as 32-bit Windows DLL files.

A few other commercial options are also available, specifically made for live acts,
like [Resolume Arena](https://www.resolume.com/) and [Magic Music Visuals](https://magicmusicvisuals.com/).

Apart from the above, there's really not much available, and most of the classic visualizers are clearly outdated and
some will even cease to work at some point, for example AVS is already mostly defunct due to its 32-bit architecture and
inherent security issues regarding the community-provided DLLs you'd have to trust not to contain any malicious code.

We think it's about time to imagine a new visualizer that uses modern technology, provides the freedom of creativity for
users while making it available on as many platforms as possible _and_ safe to use.

## Design Goals And Limitations

### Constraints

We're sure y'all have so many ideas and suggestions we should put into this project! We still have to set a few
constraints and design goals for both the technology and the features, which will possibly limit a few things. Here's a
quick overview on the hard constraints we want to enforce:

- It must work on all major desktop platforms (Windows, Linux, macOS) and CPU architectures (x86_86 and aarch64 as a
  minimum)
- Using a modern, portable 3D API is key, e.g. Vulkan (or Metal, either native or via MoltenVK), possibly WebGPU for
  browsers once the standard is no longer a draft.
- No native code and/or access to native APIs or local filesystem data allowed via presets.
- Released under a strong copyleft license, e.g. LGPL, to ensure the code (and any changes made to it) always stays
  open and accessible.
- Run on embedded platforms as well, e.g. Android smartphones and the Raspberry Pi. It would be okay to only support a
  subset of presets which don't need a big desktop GPU to work.

Apart from the above points, we're open for any suggestions.

### How It Should Look Like

To make the visualizer as versatile as possible, we want to use a similar approach as libprojectM. This means the core
visualizer is developed as a library with a slim C API to control the visuals from the outside and enable integration
into a multitude of different programming languages and environments.

The core library should be viewed like a 3D engine in a game. You feed a scene (a preset) and audio data to it, and the
engine renders the scene frame by frame. Depending on the complexity of such presets, the library may provide API access
to the internal scene structure and ways to manipulate/change it in real time.

Surrounding this library, there would be a standalone reference application similar
to [projectMSDL](https://github.com/projectM-visualizer/frontend-sdl2), additional examples and wrappers for other
languages as well as a special preset editor application to aid in creating the new presets.

We also hope that there will be an ever-growing community around this ecosystem to provide more applications and
presets.