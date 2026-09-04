# Visual Search Workbench

A native macOS app that searches the folders you choose — by text, or by a picture
you drop on it — and keeps gallery bytes on the machine.

**[Download the latest release →](https://github.com/darce/visual-search-workbench/releases/latest)**

More about the design and the reasoning behind it:
[darce.xyz/projects/visual-search-workbench](https://darce.xyz/projects/visual-search-workbench/)

This repository distributes the built application and nothing else. There is no
source here. It exists so that a published download link keeps working, stays
versioned, and can be checked against a digest.

## Requirements

| | |
|---|---|
| Mac | **Apple silicon only.** There is no Intel build; an Intel Mac cannot open it. |
| macOS | 14.0 Sonoma or later |
| Download | ~295 MB disk image |
| Installed | ~330 MB — the models are inside the app, not downloaded later |

## Two things to know first

Both follow from this being independent work rather than a shipped commercial
product. Neither is a defect, and you should decide about them before you
download 295 MB.

### It is not notarized by Apple

Notarization requires a paid Apple Developer Program membership this project does
not hold, so the app is ad-hoc signed and macOS will refuse the first double-click.

Apple's own override opens it: **System Settings → Privacy & Security**, scroll to
the message naming the app, then **Open Anyway**. You do this once.

If you would rather not run software Apple has not checked, that is a reasonable
place to stop, and no argument here is meant to talk you out of it.

### Check the bytes

Every release publishes a `SHA256SUMS` file beside the disk image. GitHub's CDN
serves the download, not this project, and the digest is the only check that
covers the whole path from build to your disk:

```
shasum -a 256 -c SHA256SUMS
```

Run it in the folder holding both files. `OK` means you received what was built.
Anything else means stop and do not open the image.

## What it does

- **Search by text or by image.** Describe what you want, or drop a photo in and
  find its visual neighbours. Searching by picture is the capability macOS Photos
  does not offer.
- **Reads only the folders you pick.** Images stay where they are.
- **Runs offline.** The embedding, segmentation, and detection models ship inside
  the app, so nothing is fetched on first launch and the app has no reason to open
  a socket.
- **Says what it does not know.** Missing, partial, and unavailable data each get a
  named state, so an incomplete view of a library never reads as a complete one.

## Bundled models and their licences

The disk image redistributes third-party model weights. Each is permissively
licensed and carries its attribution inside the app bundle, at
`Contents/Resources/LICENSE-NOTICES.md` and
`Contents/Resources/sis-models/LICENSES/`.

| Component | Role | Licence | Upstream |
|---|---|---|---|
| OpenCLIP ViT-B/32, LAION-2B | text and image embeddings | Apache-2.0 | [`laion/CLIP-ViT-B-32-laion2B-s34B-b79K`](https://huggingface.co/laion/CLIP-ViT-B-32-laion2B-s34B-b79K) |
| MobileSAM, Core ML export | segmentation | Apache-2.0 | [ChaoningZhang/MobileSAM](https://github.com/ChaoningZhang/MobileSAM) via [john-rocky/SamKit](https://github.com/john-rocky/SamKit) v1.0.0 |
| LibreYOLOX-Nano | object detection | Apache-2.0 | [`LibreYOLO/LibreYOLOXn`](https://huggingface.co/LibreYOLO/LibreYOLOXn), originating in [Megvii-BaseDetection/YOLOX](https://github.com/Megvii-BaseDetection/YOLOX) |
| open_clip BPE vocabulary | tokenization | Apache-2.0 | [mlfoundations/open_clip](https://github.com/mlfoundations/open_clip) |
| Natural Earth 110m land and coastline | offline basemap behind Places | Public domain | [nvkelso/natural-earth-vector](https://github.com/nvkelso/natural-earth-vector) |

Model weights are pinned by upstream revision and verified by SHA-256 at build
time, so a given release always contains the same weights.
