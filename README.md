# Match-3 Prototype (Images)

This small Match-3 prototype uses an HTML canvas and image tiles (watches in the example). The interactive game is implemented in index.html at the repo root.

What this README explains
- Where to edit which watch images are used.
- How to change board dimensions (grid size) and tile size.
- How to use local images to avoid CORS issues.

Files
- index.html — main game file. Open it to edit images, board size and tile size.

Where to edit the watches (tiles)
- Open index.html and find the imageFiles array near the top. It looks like this:

  const imageFiles = [
    "https://.../brown-watch.jpg",
    "https://.../blue-watch.jpg",
    "https://.../black-watch.jpg",
    "https://.../white-watch.jpg"
  ];

- Replace any URL in that array with your desired image URL. Each grid cell stores the image URL string; matching logic compares those strings, so using the same URL (or path) means the tiles are considered identical.

Using local images (recommended to avoid CORS)
- To avoid CORS or remote-loading problems, add your images to an img/ folder in the repo (for example: img/brown.jpg, img/blue.jpg). Then update the imageFiles array to reference those local paths:

  const imageFiles = [
    "img/brown.jpg",
    "img/blue.jpg",
    "img/black.jpg",
    "img/white.jpg"
  ];

- Local images remove crossOrigin concerns and let the canvas be used for export or pixel operations.

How to change the board dimension and tile size
- In index.html you will find two constants at the top that control board layout:

  const size = 4;       // number of rows and columns (4 means 4x4 board)
  const tileSize = 110; // tile size in pixels

- To make the board larger or smaller change size. For example, size = 6 yields a 6x6 board.
- If you change tileSize you should also make sure the canvas element matches the computed width and height. The script in index.html currently sets canvas.width = size * tileSize and canvas.height = size * tileSize automatically when tileSize or size are changed.

Notes on image scaling and appearance
- Images are center-cropped and scaled to cover the tile area. For best visual results use square images or images larger than the tileSize.
- The code clips images to a rounded rectangle tile shape. You can edit corner rounding in the roundRect calls inside draw() if you want sharper or rounder tiles.

Fallback colors
- If an image fails to load (or CORS prevents drawing into canvas), the code falls back to a set of solid colors (fallbackColors). You can edit fallbackColors in index.html to change these.

CORS and remote images
- index.html sets img.crossOrigin = "anonymous" when loading remote images. If the remote server does not provide Access-Control-Allow-Origin headers, some browsers may block loading with crossOrigin and the code will fall back to a solid color for that tile.
- To guarantee usage without CORS issues, host the images locally in the repo (see section above) or serve them from a domain that includes proper CORS headers.

Other places you might want to tweak
- Selection outline and tile background colors are defined in draw() and in the CSS at the top of index.html (canvas background and body styles).
- match detection and game rules are in findMatches() and resolveMatches(); changing how matches work (e.g., different run length) requires adjusting those functions.

Credits
- Prototype by the repository owner.

---

(End of README.md)