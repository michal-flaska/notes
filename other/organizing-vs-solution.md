# organizing Visual Studio solutions

Let's say that you are developing a game cheat and having a github repo for it, and that cheat consists of two projects -> cheat and kernel driver. Then: You want only one `.sln` (solution) file at the root with two `.vcxproj` (project) files - one for the driver, one for the cheat.

Structure it like this:

```
YourRepo/
│
├── YourProject.sln
│
├── Driver/
│   ├── Driver.vcxproj
│   ├── [source files]
│   └── ... other microsoft bloatware
│
└── Cheat/
    ├── Cheat.vcxproj
    ├── [source files]
    └── ... other microsoft bloatware
```

## How to actually achieve this?

In Visual Studio:
1. Create the solution at repo root
2. Right-click solution → Add → New Project (for driver)
3. Right-click solution → Add → New Project (for cheat)

This keeps both projects under one solution so you can build/manage them together while keeping the code separated. The `.sln` file references both `.vcxproj` files.

> [!NOTE]
> If you need shared code between them, add a third project as a static library and reference it from both.