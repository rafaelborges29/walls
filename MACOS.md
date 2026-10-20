# Rotate wallpapers on macOS

macOS can automatically cycle through a local folder of images without an extra
app. Follow these steps on your Mac. Settings labels vary between macOS versions;
check your version under **Apple menu > About This Mac**.

## Download the wallpapers

Use Terminal with Git installed to download only these categories: `aerial`,
`apeiros`, `architecture`, `basalt`, `cold`, `digital`, `dreamcore`, `fogsmoke`,
`minimal`, `monochrome`, `mountain`, `nature`, `nord`, and `stalenhag`.

```sh
mkdir -p ~/Pictures
cd ~/Pictures
git clone --depth 1 --filter=blob:none --sparse https://github.com/rafaelborges29/walls.git
cd walls
git sparse-checkout set aerial apeiros architecture basalt cold digital dreamcore \
  fogsmoke minimal monochrome mountain nature nord stalenhag
```

The sparse checkout selects which category folders are downloaded; other
wallpaper categories are left out. Each `git sparse-checkout set` replaces the
previous folder selection locally without changing anything on GitHub.

If macOS prompts you to install Command Line Tools for Git, finish that
installation and run the commands again. If you already cloned the repository,
run `cd ~/Pictures/walls` and the `git sparse-checkout set` command above instead
of cloning again.

## Combine the images into one folder

Run this from the downloaded `walls` folder. It copies the images from all the
selected categories into `~/Pictures/Wallpaper Mix`, with no subfolders:

```sh
cd ~/Pictures/walls
mkdir -p "$HOME/Pictures/Wallpaper Mix"
for category in aerial apeiros architecture basalt cold digital dreamcore \
  fogsmoke minimal monochrome mountain nature nord stalenhag; do
  for image in "$category"/*; do
    case "$image" in
      *.jpg|*.jpeg|*.png|*.webp)
        cp -n "$image" "$HOME/Pictures/Wallpaper Mix/$category-${image##*/}"
        ;;
    esac
  done
done
```

The category prefix prevents images from different categories with the same
filename from overwriting each other. `cp -n` skips existing destination files,
so rerunning the command adds missing images without replacing your copies.
README files are excluded, and the original images stay in the repository.

The combined folder uses additional disk space. To get new images later, run
`git pull --ff-only` from `~/Pictures/walls`, then rerun the copy commands. Existing
copies are not updated or removed automatically. Keep `Wallpaper Mix` in place
so macOS can continue using it. If an image format is not offered in Wallpaper
settings, use a JPG or PNG version of that image.

## Enable desktop rotation

1. Open **Apple menu > System Settings > Wallpaper**.
2. Under **Your Photos**, choose **Add Photo > Choose Folder**. On versions that
   show **Add Folder or Album**, use **Add Folder** instead.
3. Select **Pictures > Wallpaper Mix**, then click **Choose** or **Open**.
4. Select the folder's **Shuffle** / rotating-arrows tile instead of an individual
   image. Choose a change interval, such as every 5 minutes, from the controls
   near the current wallpaper preview. Enable random order if your version offers
   that option.
5. Enable **Show on all Spaces** if you want the same wallpaper across desktops
   and displays.

Leave the desktop visible for one interval to verify that the image changes. To
stop rotation, select a single image in Wallpaper settings.

## Lock screen and photo slideshow

The normal lock screen generally follows your desktop wallpaper, although its
appearance also depends on your screen saver. Lock the logged-in Mac with
**Control-Command-Q** to check it. The login screen after logout or restart,
including FileVault's startup unlock screen, can look different; desktop rotation
does not configure a separate startup slideshow.

To cycle through photos while the Mac is idle or locked, configure a photo screen
saver separately:

1. In **System Settings > Wallpaper**, open **Screen Saver** and select **Custom**.
   If your version has a separate **Screen Saver** sidebar item, open that instead.
2. Select **Photos** under **Other**, then open **Options > Choose Folder** and
   select the same image folder. Older versions may offer photo styles such as
   **Shifting Tiles**, with the folder selected under **Source**.
3. In **System Settings > Lock Screen**, set when the screen saver starts. Choose
   a display-off delay longer than that if you want time to see the slideshow,
   and set **Require password after screen saver begins or display is turned off**
   to **Immediately**.
4. Preview the screen saver, then lock the Mac and wait for its start delay to
   verify it. The slideshow stops being visible when the display sleeps; its
   timing and image order are separate from desktop rotation.

## Apple references

- [Customize the wallpaper on your Mac](https://support.apple.com/guide/mac-help/mchlp3013/mac)
- [Wallpaper settings](https://support.apple.com/guide/mac-help/mchlp1103/mac)
- [Use photos as your screen saver](https://support.apple.com/guide/mac-help/mchle95c1370/mac)
- [Lock the screen of your Mac](https://support.apple.com/guide/mac-help/mchl8e8b6a34/mac)
