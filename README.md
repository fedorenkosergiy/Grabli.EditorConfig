# Grabli.EditorConfig

Editor config for Unity3d packages and/or projects

## How to use?

The main idea is to attach this project to your and use symlinks to have [`.editorconfig`](.editorconfig) at a
correct place.

The project contains two branches that can be used in other projects.
These are [`pure`](https://github.com/fedorenkosergiy/Grabli.EditorConfig/tree/pure) 
and [`main`](https://github.com/fedorenkosergiy/Grabli.EditorConfig/tree/main).

[`pure`](https://github.com/fedorenkosergiy/Grabli.EditorConfig/tree/pure) 
contains [`.editorconfig`](.editorconfig) file only

[`main`](https://github.com/fedorenkosergiy/Grabli.EditorConfig/tree/main)
contains full package files set.

If you develop a [custom unity3d package](https://docs.unity3d.com/Manual/CustomPackages.html)
it's best to use [`pure`](https://github.com/fedorenkosergiy/Grabli.EditorConfig/tree/pure) branch
to avoid GUID conflicts if a package user has other packages dependent on this one.

If you work on a final product you can use both branches.
But it's recommended to attach this project as a [unity3d package](https://docs.unity3d.com/Manual/Packages.html)
and aim your symlinks to a copy of the package 
in the [Library/PackageCache](https://docs.unity3d.com/Manual/upm-embed.html) directory.

Btw, to create a symlink use the following command template
```shell
ln -s source_file symbolic_link
```

For example, if you attached this editorconfig as a package 
and you want to use the [`.editorconfig`](.editorconfig) file as a config to the whole project 
then the command may look like this

```shell
cd my-project-root-path
ln -s Library/PackageCache/fedorenkosergiy.grabli.editorconfig@636ebb2/.editorconfig .editorconfig
```

### As a submodule
If you use [git](https://git-scm.com/) as a VCS
you can use [submodules](https://git-scm.com/docs/git-submodule) approach to attach this project to your.

The best place to put the submodule at is somewhere out of Assets and Packages directory 
to avoid unnecessary importing by unity.

Use following commands to attach this project as a submodule.
Replace `my-parent-directory-path` with your path and `branch-name` with the branch name you prefer.
```shell
cd my-parent-directory-path
git submodule add git@github.com:fedorenkosergiy/Grabli.EditorConfig.git
cd Grabli.EditorConfig
git checkout branch-name
```

### As a unity package
Select the version of the package you prefer.
It's best to use static references like exact commits and tags.
The less reliable approach is to use a reference to a branch name or the head.
But if you're aware of possible issues I have no power to stop you :wink:

The next step is combining the package source URL and the version marker.
For example, 
if you want to use version [`v0.0.1`](https://github.com/fedorenkosergiy/Grabli.EditorConfig/releases/tag/0.0.1)
it would be this line you need
```
https://github.com/fedorenkosergiy/Grabli.EditorConfig.git#v0.0.1
```
One more example.
If you want to use commit 
[`636ebb221b51032fc328157f86af6f7f722feaea`](https://github.com/fedorenkosergiy/Grabli.EditorConfig/commit/636ebb221b51032fc328157f86af6f7f722feaea)
it would be this line you need
```
https://github.com/fedorenkosergiy/Grabli.EditorConfig.git#636ebb221b51032fc328157f86af6f7f722feaea
```

So, now when you have a pointer to the version you need it's time to attach the package to your project.
Open [`Packages/manifest.json`](https://docs.unity3d.com/Manual/upm-manifestPrj.html) file.
Add there following line among other similar lines
```
"fedorenkosergiy.grabli.editorconfig": "https://github.com/fedorenkosergiy/Grabli.EditorConfig.git#version-marker",
```

Here is an example
```
...
"com.unity.2d.sprite": "1.0.0",
"fedorenkosergiy.grabli.editorconfig": "https://github.com/fedorenkosergiy/Grabli.EditorConfig.git#v0.0.1",
"com.unity.2d.tilemap": "1.0.0",
...
```

As an option you can also use [package manager window](https://docs.unity3d.com/Manual/upm-ui.html) to add the package manually

## How to collaborate?
There is no way for now. But I'm thinking of that