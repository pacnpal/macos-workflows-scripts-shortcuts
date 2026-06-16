# macOS Workflows, Scripts, and Shortcuts

Small macOS automations I've built and decided to share. Quick Actions, shell scripts, and Shortcuts. Each one fixes a specific annoyance, and each has its own README with what it does and how to install it.

There's one thing in here right now. More will show up as I make them.

## What's in here

### Workflows

**[Remove Quarantine](workflows/Remove-Quarantine)** is a Quick Action that strips the `com.apple.quarantine` flag off files and folders, then ad-hoc re-signs broken app bundles so they'll open on Apple Silicon. Right-click an app, pick it from Quick Actions, and the "app is damaged and can't be opened" error goes away. Read its README for install steps.

## How it's organized

Everything is grouped by type:

```
workflows/    Automator Quick Actions and other .workflow bundles
scripts/      shell scripts
shortcuts/    Shortcuts app shortcuts
```

So far only `workflows/` has anything in it. Each item gets its own folder with a README and the file you download.

## License

MIT. Do what you want with it. See [LICENSE](LICENSE).
