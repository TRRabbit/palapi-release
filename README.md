# PalApi

PalApi is a mod loader for your **Palworld dedicated server**. It lets you run server-side plugins
(auto-save, chat commands, protections, that kind of thing) without touching the players - people
join with the normal vanilla game, they dont need anything installed on their side.

It only runs on the server. Your world, your save, your players: untouched.

> This is an early release. It works and it has been tested a lot, but treat it like a beta and keep
> a backup of your save (you should be doing that anyway).

## What you need

- A Palworld **dedicated server** running on Windows (the SteamCMD one, `PalServer`).
- Nothing else. No .NET, no runtime to install.

## Install (the easy way - drop-in)

1. Download the zip from the Releases page and unzip it somewhere.
2. Open your server folder and go into:
   `Pal\Binaries\Win64\`
   (thats the folder with `PalServer-Win64-Shipping-Cmd.exe` in it)
3. Copy **`version.dll`** into that folder, right next to the exe.
4. Copy the **`palapi.cfg`** file into the same folder (optional, but nice to have).
5. Copy the **`PalApi`** folder (the one with `Plugins` inside) into the same folder too.
6. Start your server like you always do.

Thats it. PalApi loads itself when the server boots.

Your Win64 folder should end up looking like this:

```
Pal\Binaries\Win64\
    PalServer-Win64-Shipping-Cmd.exe
    version.dll            <- PalApi
    palapi.cfg             <- PalApi (optional)
    PalApi\
        Plugins\           <- your plugins go here
```

## Check that it worked

After the server started, look in the `Win64` folder for a new file called **`palapi.log`**.
Open it, near the top you should see a line like:

```
compat: build=... => COMPATIBLE
```

If you see `COMPATIBLE`, youre good. PalApi even re-checks itself every time Palworld updates, so a
game patch usually doesnt break it.

If the file isnt there, double check `version.dll` is really in the same folder as the server exe.

## Adding plugins

Put each plugin in its own folder under `PalApi\Plugins\`, like:

```
PalApi\Plugins\MyPlugin\MyPlugin.dll
PalApi\Plugins\MyPlugin\PluginInfo.json
```

Restart the server and it picks them up. You can also swap a plugin while the server runs (drop a
`.dll.palapi` file), but a restart is the simple way.

## Other install method (launcher)

If you'd rather not drop a dll in the game folder, the zip also has **`PalApiLoader.exe`** +
**`PalApiCore.dll`**. Instead of starting the server the normal way, you start `PalApiLoader.exe` and
it launches + loads the server for you. Same result, just injected a bit earlier. Most people dont
need this, the drop-in `version.dll` is simpler.

## Removing it

Delete `version.dll` (and the `PalApi` folder and `palapi.cfg` if you want). Server goes back to
100% vanilla. Nothing else is changed on your machine.

## A small ask

PalApi is free and made for the community. If you like it, please **dont resell it** - its free for
everyone anyway - and if you build something cool on top of it, share it back so everybody gets it.

## Something broke?

Turn on the detailed log: open `palapi.cfg` and set `debug_log=true`, restart, then check
`palapi_debug.log`. That file usually tells you whats going on. Bug reports and questions are
welcome on the issues page.
