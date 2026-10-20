# Rotate wallpapers on macOS

macOS can automatically cycle through a local folder of images without an extra
app. Follow these steps on your Mac. Settings labels vary between macOS versions;
check your version under **Apple menu > About This Mac**.

## Download the wallpapers

For the whole collection, open [this repository](https://github.com/rafaelborges29/walls),
choose **Code > Download ZIP**, and extract it. Allow roughly 3.5 GB for the
extracted files, plus space for the ZIP; the collection can grow.

To download only selected categories instead, use Terminal with Git installed:

```sh
mkdir -p ~/Pictures
cd ~/Pictures
git clone --depth 1 --filter=blob:none --sparse https://github.com/rafaelborges29/walls.git
cd walls
git sparse-checkout set nature minimal mountain
```

Replace `nature minimal mountain` with the category folders you want. If macOS
prompts you to install Command Line Tools for Git, finish that installation and
run the commands again. Run `git pull --ff-only` from the `walls` folder later to
get updates.

## Choose one folder or mix categories

For a single category, use its folder directly, such as `walls/nature`.

For a mix, create a folder such as `Pictures/Wallpaper Mix` in Finder and copy
your chosen images into it. Put the image files directly inside that folder,
rather than adding category subfolders. Review any duplicate-filename prompts
when copying from multiple categories. Copies use additional disk space and do
not automatically receive repository updates.

Keep the chosen folder in a permanent local location. Start with still images
such as JPG and PNG; the `animated` category is not a built-in video wallpaper
playlist.

## Enable desktop rotation

1. Open **Apple menu > System Settings > Wallpaper**.
2. Under **Your Photos**, choose **Add Photo > Choose Folder**. On versions that
   show **Add Folder or Album**, use **Add Folder** instead.
3. Select your category folder or `Wallpaper Mix`, then click **Choose** or
   **Open**.
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
