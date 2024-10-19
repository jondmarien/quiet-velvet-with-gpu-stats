
<div align="center">

# Quiet Velvet 🌸

**Quiet Velvet is a custom task bar using [Zebar](https://github.com/glzr-io).**

⬇️ Join the community ⬇️

[![Discord invite][discord-badge]][discord-link]

If you need help, send me a message on discord, my ID is `0h37`.

![demo-quiet-velvet](https://raw.githubusercontent.com/LeoBessin/files/refs/heads/master/zebar/my_custom_zebar.gif)

</div>

## Installation 📂

Go to your `~/.glzr/zebar/` folder then clone this repository.
- ```git clone https://github.com/LeoBessin/quiet-velvet```

Enter the repository and install the dependencies.
- ```cd ./quiet-velvet/```
- ``npm install``

- Create a `config.js` file in the `./src/` folder. You can configure it later with the [configuration](#configuration) section.

Then build the project with this command.
- ```npm run build```

After these steps you need to reload the Zebar's config.

You should see quiet-velvet/main in Widget configs !

![zebar-update](https://raw.githubusercontent.com/LeoBessin/files/refs/heads/master/zebar/reload_zebar.png)

[discord-badge]: https://img.shields.io/discord/1041662798196908052.svg?logo=discord&colorB=7289DA
[discord-link]: https://discord.gg/ud6z3qjRvM

## Configuration ⚙️

You need to create a `config.js` file in the directory `quiet-velvet/src/`.
Enter the following key/values in the file. 

I will explain how to get all the Spotify tokens in the section [Spotify](#spotify).

```js
export default {
    spotifyClientId: '<YOUR-SPOTIFY-CLIENT-ID>',
    spotifyClientSecret: '<YOUR-SPOTIFY-CLIENT-SECRET>',
    spotifyRefreshToken: '<YOUR-SPOTIFY-REFRESH-TOKEN>',
    explorerPath: '<YOUR-EXPLORER-PATH>',
    powershellPath: '<YOUR-POWERSHELL-PATH>'
}
```

## Customization 💅

You can change the style by editing these values of the `styles.css` file.
- Main color : `--main-color`  .
- Font color : `--font-color`.
- Background : `--background-color`.

If you use GlazeWM, you can change the names of your workspaces in the `~/.glzr/glazewm/config.yaml`:
```yaml
workspaces:
  - name: "1"
    display_name: "[discord-logo] Other"
    ...
  - name: '2'
    display_name: "[code-logo] Work"
    ...
  - name: '3'
    display_name: "[search-logo] Search"
    ...
...
```
Replace the [xxx-logo] by one of https://www.nerdfonts.com/cheat-sheet.


## Widgets 📦

For the time being, Quiet Velvet only has 4 widgets.
- [Spotify](#spotify)
- [Google Search](#google-search)
- [Shortcut](#shortcut)
- [Settings](#settings)

### Spotify
![quiet-velvet-spotify](https://raw.githubusercontent.com/LeoBessin/files/refs/heads/master/zebar/spotify_zebar.png)

> This widget display your current playing Spotify song.
> 
> **On hover**, you will have access to previous, play/pause and skip song.
> 
> **On click**, it will open the spotify app.

To use this widget, you need to follow a few simple steps.
1. Go to your [Spotify developer dashboard](https://developer.spotify.com/dashboard).
2. Create an app with whatever name and description and add this URI in the Redirect URIs section :
   https://alecchen.dev/spotify-refresh-token. Choose the `Web API` option.
3. Open your new app option and fill the `spotifyClientId` and `spotifyClientSecret` values of the `src/config.js`.
4. Go to https://alecchen.dev/spotify-refresh-token/ and fill your client id and your client secret then choose the 
   following options : `user-read-currently-playing`, `user-modify-playback-state` and `streaming`.
5. Hit submit and fill the `spotifyRefreshToken` value of `src/config.js`.

The widget will automatically generate Spotify access token, store them in local storage and generate another one if 
the precedent expires.

### Google Search
![quiet-velvet-google-search](https://raw.githubusercontent.com/LeoBessin/files/refs/heads/master/zebar/google_search_zebar.png)

> With this widget you can quickly search any information on google.
> 
> **When the key enter is pressed** it will focus the GlazeWM workspace 3 and open your explorer.

To use this widget, you only need to fill the `explorerPath` value of `src/config.js`.

You can change or remove the focusing workspace in the function `onSubmit` of the file `src/components/GoogleSearch.
jsx`.

### Shortcut
![quiet-velvet-shorcuts](https://raw.githubusercontent.com/LeoBessin/files/refs/heads/master/zebar/shortcuts_zebar.png)

> This widget lets you execute a shortcut like opening an application or a website.
> 
> **On click** it will execute the shortcut.

To create a shorcut follow this example :
```jsx
<Shortcut commandRunner={output.glazewm.runCommand}
          commands={[
              'focus --workspace 2',
              `shell-exec ${config.powershellPath}`
          ]}
          iconClass="nf-cod-terminal_powershell" name="Powershell"
/>
```
You can add a key/value in the `src/config.js` and use it here like here with the `powershellPath`.

To change the icon choose one from https://www.nerdfonts.com/cheat-sheet anc paste the class in the `iconClass` 
property.

### Settings
![quiet-velvet-settings](https://raw.githubusercontent.com/LeoBessin/files/refs/heads/master/zebar/settings_zebar.png)

> This widget lets you change the visibility of all your widgets and keep your choices on local storage.

If you want to add another widget follow this example :
```jsx
function App() {
    const [showXWidget, setShowXWidget] = useState(true);
    const [showYWidget, setShowYWidget] = useState(true);
    ...
    return (
        <>
            ...
            {showXWidget ? <XWidget/> : null}
            ...
            {showYWidget ? <YWidget/> : null}
            ...
            {<Settings widgetObj={[
                { name: 'XWidget', changeState: setShowXWidget },
                { name: 'YWidget', changeState: setShowYWidget }
            ]}/>}
            ...
        </>
    )
}
```
Click on the gear logo then change the state of the widget.

## Tips 🎁
- You can open your task manager by clicking on the memory or cpu logo.
- You can change the date format by hovering it.
