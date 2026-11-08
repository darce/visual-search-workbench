# Visual Search Workbench

A native macOS app for finding photos in the folders you choose: search by text
or by a picture, explore dates and places, and make experimental cutouts.
Search and the bundled models run on your Mac.

**[Download the latest release](https://github.com/darce/visual-search-workbench/releases/latest)**
· **[0.2.9 release notes](https://github.com/darce/visual-search-workbench/releases/tag/v0.2.9)**
· [Project and design notes](https://darce.xyz/projects/visual-search-workbench/)

This repository distributes the built app and its documentation. Application
source is not included.

## Download and install

The current release is **0.2.9**.

| Requirement | Details |
|---|---|
| Mac | Universal build: Apple silicon and Intel. Native validation was performed on Apple silicon. |
| macOS | 14.0 Sonoma or later |
| Download | Approximately 300 MiB |
| Installed app | Approximately 333 MiB, including the models |

1. Download [**VisualSearchWorkbench-0.2.9.dmg**](https://github.com/darce/visual-search-workbench/releases/download/v0.2.9/VisualSearchWorkbench-0.2.9.dmg).
2. Open the disk image and drag **Visual Search Workbench** to **Applications**.
3. Open the app, choose your photo folders, and index them before searching.

The search, segmentation and object-detection models are included. No model
download or model-folder setup is needed for the release app.

### Signing and first launch

The app is signed with an **Apple Development identity** and is **not notarized
by Apple**. macOS may block its first launch. Use **System Settings → Privacy &
Security**, find the message naming the app, and choose **Open Anyway**.

### Check the download

Download [SHA256SUMS](https://github.com/darce/visual-search-workbench/releases/download/v0.2.9/SHA256SUMS)
into the same folder as the disk image, then run:

```sh
shasum -a 256 -c SHA256SUMS
```

An `OK` result confirms that the disk image matches the published checksum.

Only the DMG is needed to install. GitHub automatically attaches **Source code**
ZIP and tar archives to every release; those contain the files in this download
repository, not the application source.

## What you can do

- **Search by text or image.** Describe a photo or drop in a picture to find
  visual neighbours.
- **Explore dates and places.** Narrow results with the Timeline and Places
  views while keeping the accepted results visible during updates.
- **Inspect the original.** Keep results beside a selected-photo inspector,
  see the photo's original location, and use **Show in Finder**.
- **Make cutouts.** Experimental segmentation creates saved layers. Cutout jobs
  run one photo at a time, with queued status and per-photo cancellation.
- **Recover an incomplete index.** Successfully indexed photos remain usable
  after cancellation or individual failures. Recorded failed photos have an
  explicit retry action.
- **Compare two photos.** Experimental **Compare blur** supports manual A/B
  region inspection. It does not provide automatic best-shot ranking or
  calibrated blur-quality scores.

### What's new in 0.2.9

This download includes the changes prepared for 0.2.7 and 0.2.8.

- Fixes repeated Resume attempts that made no indexing progress, and makes
  failed-photo recovery visible.
- Improves search status, selected-photo actions, cutout-job feedback and
  thumbnail selection.
- Adds a responsive comparison layout with **Choose A** and **Retry A**
  recovery, plus a measured admission path for supported JPEG/PNG originals.
- Includes Timeline cancellation and stale-result fixes, queued cutouts,
  folder-access improvements, and a fix for the text-search Core ML GPU crash.

See the [release notes](https://github.com/darce/visual-search-workbench/releases/tag/v0.2.9)
for the full change list and validation scope.

## Privacy and optional network features

Photos stay in their chosen folders. Text search, image search, segmentation and
object detection run locally using the bundled models.

These network features are **off until you enable them**:

| Feature | What enabling it does |
|---|---|
| Apple MapKit basemaps | Fetches online map content. The bundled Natural Earth basemap works offline. |
| Layer naming through local Ollama | Contacts an Ollama service on your Mac. |
| Layer naming through a server you specify | Sends reduced copies of photos to that server after consent. |

Photo-location storage has its own privacy setting and purge action. Review the
app's privacy settings before enabling optional services.

## Experimental comparison limits

The expanded measured-camera comparison path accepts **opaque RGB8 JPEG/PNG**
originals with EXIF orientation **1 or 6**, up to **3,264 pixels per edge** and
**7,990,272 source pixels**, within its measured resource limits.

Existing primary-HEIF preview support remains; expanded HEIF comparison
admission is unavailable. Unsupported or unreadable inputs may require
choosing another photo or retrying. The smallest comparison-window layout and
OS keyboard/VoiceOver behavior remain unverified. A full-suite 0.2.9 rerun was
not completed; focused native, regression and resource checks, documentation
checks, universal packaging, signature checks and an isolated launch smoke
check are recorded in the release evidence.

## Software licence

The first-party app uses the **[VSW Personal and Internal Use terms](LICENSE)**,
based on PolyForm Internal Use 1.0.0 with an additional personal-use permission.

Personal, noncommercial use and your own internal business use are permitted.
Redistribution, repackaging into another product, or providing an externally
offered service requires separate permission. Attribution alone does not grant
those rights.

Commercial licensing or support for otherwise permitted use is optional; the
terms impose no usage, seat, revenue or installation-count threshold.
[NOTICE](NOTICE) identifies first-party and third-party scope. The same terms
ship inside the app at `Contents/Resources/VSW-LICENSE.txt`.

## Bundled models and their licences

Third-party components retain their own terms. The app includes the full
inventory at `Contents/Resources/LICENSE-NOTICES.md`, with licence texts and
attribution alongside the models.

| Component | Role | Licence | Upstream |
|---|---|---|---|
| OpenCLIP ViT-B/32, LAION-2B | Text and image embeddings | MIT, declared by the pinned model card | [laion/CLIP-ViT-B-32-laion2B-s34B-b79K](https://huggingface.co/laion/CLIP-ViT-B-32-laion2B-s34B-b79K/tree/1a25a446712ba5ee05982a381eed697ef9b435cf) |
| MobileSAM, SamKit v1.0.0 Core ML export | Experimental segmentation | Apache-2.0 | [MobileSAM](https://github.com/ChaoningZhang/MobileSAM) via [SamKit v1.0.0](https://github.com/john-rocky/SamKit/releases/tag/v1.0.0) |
| LibreYOLOX-Nano | Object detection | Apache-2.0 | [LibreYOLO/LibreYOLOXn](https://huggingface.co/LibreYOLO/LibreYOLOXn), originating in [YOLOX](https://github.com/Megvii-BaseDetection/YOLOX) |
| CLIP BPE vocabulary, redistributed by open_clip | Tokenization | MIT | [OpenAI CLIP](https://github.com/openai/CLIP) and [open_clip](https://github.com/mlfoundations/open_clip) |
| Natural Earth 110m land and coastline | Offline basemap | Public domain | [Natural Earth vector data](https://github.com/nvkelso/natural-earth-vector) |

Model payloads are pinned and verified by SHA-256 during packaging. The
OpenCLIP model card declares MIT but supplies no weight-specific licence text
or copyright holder; the relevant OpenAI CLIP and open_clip MIT notices ship
with the app. MobileSAM/SamKit and detector licences and notices are included
separately.
