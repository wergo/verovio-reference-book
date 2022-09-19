---
title: "History of the project"
---

Engraving music notation by computer is a notoriously complex task, and the most powerful music notation rendering engines are, for the most part, the result of long-term developments of commercial music notation editors in which considerable resources had to be invested. They each have their own internal structure and file formats. Furthermore, the music notation rendering engines of music notation editors are not very modular and cannot easily be used or integrated into other applications.

Besides music notation editors, some music notation rendering engines are also available as command-line tools. These are easier to integrate than desktop applications, however with occasionally quite significant dependencies and requirements that limit the contexts in which their use is possible. This is the case for [LilyPond](http://lilypond.org/), a very popular and powerful typesetting engine

Such tools have been used for many years within the [Music Encoding Initiative](https://music-encoding.org) (MEI) community for engraving scores encoded in MEI. Using them, however, meant converting the MEI to another encoding scheme that could be used as input format for the engraving tool. Whichever solution was used to do this, it remained clearly suboptimal. MEI users willing to benefit from all the strengths of MEI were facing the problem of not being able to render their data properly. Converting a music encoding format to another one is known to become quickly problematic. It is particularly true when converting from MEI markup that is rich and detailed, a feature that distinguishes MEI from other encoding schemes. With a conversion step, it is likely that not all the information will be preserved in the rendering, or at least only in cumbersome ways and with sometimes quite limited results.

At that time, by about thirty years after the initial development of music notation software applications, the digital domain had significantly changed with the advent of the online world. For music notation, this translated into new possibilities but also new challenges to be faced. While most music notation engraving tools target PDF, this format is clearly not the ideal one in web-based environments. It can be published online, but some web browsers still require a dedicated viewer plugin to be installed for this to be possible. They yield inconsistent viewing and document browsing experiences, which is far from ideal. To embed PDF files directly in web pages code, they need to be converted to images, which creates an overhead and additional complications in the publication process, with often poor results in the display quality.

### Early stages

In 2013, the [RISM Digital Center](https://rism.digital) launched the development of Verovio for rendering the music incipits or the [RISM project](https://rism.info). The main idea behind the development of Verovio was to implement a tool that could render the RISM music incipits directly but also to support MEI natively. That is, without having MEI converted to another format, either explicitly or internally in the software application used for rendering. With Verovio, the MEI markup is parsed and rendered as notation with a single tool and in one step.

One of the reasons for choosing to implement a library from scratch rather than modifying an existing library was that it will allow to operate on a memory representation of MEI, which will make it significantly easier to render complex MEI features in the long run. Previous experience has indeed shown that modifying an existing solution can be very quick to develop at the beginning, but that the development curve eventually reaches a plateau.

Another idea behind the development of Verovio was to have a tool that would be easy to use in web environments. Instead of targeting PDF output, Verovio uses the [Scalable Vector Graphics](https://www.w3.org/TR/SVG11/) (SVG) format developed and maintained by the [W3C](https://www.w3.org/). The advantage of SVG over other output formats, and Postscript and PDF in particular, is that it can easily be used in a web-based environment because it is rendered natively in most modern web browsers with no plug-in required. In addition, since SVG is a vector format, the output can also be used for high-quality printing, which means that it offers the best of both digital and paper-based worlds.

With the same goal in mind, Verovio was designed to be light and fast and has no external dependencies, making it very flexible and easy to use or integrate into digital environments.

### Interacting with music encoding

Today, partly in response to the development of MIR applications, rendering of music notation can be necessary in very different contexts, for example within standalone desktop applications, in server-side web application scenarios, or directly in a web browser. Music notation might need to be rendered for displaying search results or for visualising analysis outputs. Another example is score-following applications, where the passage currently played needs to be displayed and possibly highlighted. These are different use-cases of interactive applications where music notation plays a key role, including many cases where the notation itself has to be an interactive component.

Several design features of the Verovio library make it highly suitable for interactive music notation applications. It is a software library that can run in a wide range of environments (and not a full software application) and it is light and fast. The JavaScript version of Verovio is particularly promising because it provides a fast in-browser music MEI typesetting engine that can easily be integrated into web-based applications. This setup makes it possible to design ground-breaking web applications where the MEI encoding is rendered on the fly. In such designs we can rethink the interface and avoid mimicking page output. We can instead adjust the layout dynamically to the screen of the device employed by the user. The layout can be calculated to fill the size of the screen, or interactively changed according to a zoom level adjusted by the user. This opens up new responsive web-interfaces to be designed and developed based on dynamic music notation reflow. This works particularly well with SVG, especially since it is now supported by all modern web browsers. However innovative the dynamic layout of music notation may be, it remains a very basic interaction. Verovio aims to go further and to produce a graphic output that can then be the foundation for more complex interactions.

Because SVG is XML, it has an advantage over raster image formats in that every graphical element is addressable. This feature makes it intrinsically well suited for interaction, and this is also true for music notation. In a web environment, the addressability can be used for highlighting graphical elements such as notes or any other music symbols. One additional characteristic of SVG is that its XML tree can be structured as desired, and an innovative design feature of Verovio was to go further in the structuring of the output by leveraging this characteristic. Since Verovio implements the MEI structure internally, this key feature of SVG made it possible to preserve the MEI structure in the design of the SVG output in Verovio. Preserving the MEI structure in the SVG output is a considerable overhead in the rendering process but makes it a unique feature of Verovio.

As a result, Verovio output in SVG is not the end of a unidirectional rendering process. Quite on the contrary, it should instead be seen as an intermediate layer standing between the MEI encoding and its rendering that can act as the cornerstone for a bi-directional interaction: from the encoding to the notation, but also from the notation to the encoding through the user interface.

### Design principles

The basis for interactivity offered by MEI coupled with Verovio follows some important design principles. First for all, the principle of *availability* and *discoverability*. That is, all the content (e.g., all the MEI editorial variants) is available. Alternative text can be made discoverable, for example with CSS highlighting. It also follows the design principle of *scalability*. Verovio is light and fast. It can run on small devices, but it also supports large files in higher resource environments.

They are also some technical principles that are followed as far as possible. They include *reusability* and *durability*. By providing only the interaction foundation and not making any assumption in interface design, especially with a software library that has no dependency, reusability is undeniably maximised. So is the durability, although durability is hard to predict in software development, particularly for digital humanities projects which have slow development cycles in comparison with the development of the technology itself. Reducing dependencies as much as possible is one way to increase durability. In the case of MEI rendering, keeping the rendering engine separate from larger applications that will use it is another way.

In terms of editions and interface design, there is much still to invent. This will need to be done hand in hand with the development of MEI. It is obvious that merely imitating printed output in a digital environment will not be satisfactory. Most effort should be spent on developing the added value that digital environments can offer. Parallel with the development of the online world is the appearance of new devices, such as tablets with wireless network access. They offer new possibilities in terms of digital access and change the manner and location in which digital content can be read. Developing these possibilities will not preclude the co-existence of printed editions, which have and will continue to retain their own added value. The challenge now is neither to replicate nor to supplant existing media or applications, but to expand horizons by exploring new ways of conceiving the information to which we have access, and MEI and Verovio are a decisive and exciting step in this direction.