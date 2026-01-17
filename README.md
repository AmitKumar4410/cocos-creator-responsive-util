# Cocos Creator 3.x Responsive Util for 2D Games

A robust, plug-and-play responsive layout utility for Cocos Creator 3.x.
This library handles aspect ratio management, safe area adaptation, and specifically fixes scaling issues for Spine animations that do not work well with the standard Widget component.

# 📥 Installation
# Install via Download (Recommended)
1.  **Get the Library:**
    Download the **`responsive-util-[version].tgz`** file provided by the developer.

2.  **Add to Project:**
    Place the `.tgz` file inside your project folder (e.g., create a `libs` folder).
    
    ```text
    MyGameProject/
    ├── assets/
    ├── libs/
    │   └── responsive-util-[version].tgz  <-- Put file here
    └── package.json
    ```

3.  **Install:**
    Run this command in your terminal:

    ```bash
    npm install ./libs/cc-responsive-util-[version].tgz
    ```
# Install via GIT (Recommended)
This method allows you to use standard imports without manual file copying or path configuration.

1.  Go to the **[Releases](../../releases)** page.
2.  Right-click the **`responsive-util-[version].tgz`** file and choose **"Copy Link Address"**.
3.  Open your project terminal and run:

```bash
# Replace the URL below with the link you just copied
npm install https://github.com/AmitKumar4410/cocos-creator-responsive-util/releases/download/[version]/cc-responsive-util-[version].tgz

## ⚙️ Project Setup (Important)

Before using the library, adjust your Cocos Creator **Project Settings** to let the library handle the scaling logic:

1.  Go to **Project** -> **Project Settings** -> **Project Data**.
2.  Under **Screen Adaption**:
    * ❌ Uncheck **Fit Width**.
    * ❌ Uncheck **Fit Height**.
    * *(We recommend letting this library handle the fitting logic explicitly).*

---

## 🚀 Usage

### 1. Initialize (Entry Point)
You must initialize the library once at the start of your game (e.g., in your first scene's `onLoad`).

```typescript
import { Responsive } from 'cc-responsive-util'; // Adjust import path if needed

@ccclass('GameManager')
export class GameManager extends Component {
    protected onLoad(): void {
        // Syntax: Responsive.init(designWidth, designHeight, tolerance, forcePortrait);
        
        Responsive.init(
            720,   // Your Design Resolution Width
            1280,  // Your Design Resolution Height
            0.02,  // Tolerance (Sensitivity threshold, default 0.02)
            true   // Force Portrait: Forces portrait layout logic even if rotated
        );
    }
}

For Spine or Individual Node scaling or resize

@ccclass('BackgroundSpineAnimation')
export class BackgroundSpineAnimation extends Component {

    protected onLoad(): void {
        // 1. Fit immediately on load
        Responsive.fitToScale(this.node);

        // 2. Listen for screen resize events to keep it fitted
        view.on('canvas-resize', this.onResize, this);
    }

    protected onDestroy(): void {
        // Clean up the event listener
        view.off('canvas-resize', this.onResize, this);
    }

    private onResize() {
        Responsive.fitToScale(this.node);
    }
}

```
# Licence
Copyright © 2026. All Rights Reserved. This library is free for use in commercial projects. Redistribution or modification of the source code is prohibited.