# What is UseLatexMk

UseLatexMk is a cmake tool to build Latex documents from cmake projects.

Instead of doing the tedious work of implementing all the logic on how to
build Latex files in the CMake language (like the better known
[UseLATEX](https://github.com/kmorel/UseLATEX) does), it uses the LatexMk tool
found on the system. As a result, there are some advantages of using
UseLatexMk.cmake over using UseLATEX.cmake:

* Additional input files, like e.g. code listing, do not have to be
  manually listed anymore. Dependency tracking is done by LatexMk instead
  of cmake.
* The generation procedure is more robust, because
  it relies on an upstream tool with a wider userbase.
* Additional (sophisticated) build logic can be provided to latexmkrc
  through configuration files without touching the CMake code. Note,
  you need to do this to build non-PDF documents.
* A target `clean_latex` to clean the build directory from all latex output
  and auxiliary latex files is available.

**Please note the following two restrictions**:

UseLatexMk relies on latexmk separating input and output directory correctly.
This includes using an absolute path for the output directory. On some TeX
systems this requires the disabling of a security measure by setting `openout_any = a`.
See UseLatexMk.cmake for additional information on the matter.

UseLatexMk is mainly designed to build PDF documents. You may enable building
other types of documents by providing a custom latexmkrc template, but you may
experience incompatibilities with other parts of UseLatexMk, such as installation.

## What is needed to use UseLatexMk from my project

You just need to

* copy all the CMake modules (`*.cmake`) from this project into your project
* Include them with `include(UseLatexMk)`. This is best done from the top-level
  directory of your project, to make the `clean_latex` target available on that level.

Now, you are ready to use it!

## Usage

Just use the following CMake function `add_latex_document` from anywhere in your project.
For an explanation of parameters, check `UseLatexMk.cmake`.

To clean the build directory from all latex files, use the target `clean_latex`.

## TODO

* Test the Ninja generator (struggles with add_custom_command)

## License

This software is provided under a combined BSD/Apache license, you can find
the original upstream license in `/LICENSE-UPSTREAM` and this repository's
license in `/LICENSE`.
