# Pick Your Style

## Introduction

Since NOJ `0.5.0`, you can customize your NOJ theme. Right now it only affect navbar and footer style and can only be choosen from the following varients.

## Available Themes

<style>
    div.theme-container{
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
    }
    div.theme-pattle{
        display: flex;
        width: 10rem;
        height: 10rem;
        border-radius: 10rem;
        justify-content: center;
        align-items: center;
        margin: 1rem;
        box-shadow: inset 0 0 4px 0 rgb(0 0 0 / 14%), inset 0 3px 4px 0 rgb(0 0 0 / 12%), inset 0 1px 5px 0 rgb(0 0 0 / 20%);
    }
    div.theme-pattle > p{
        margin: 0;
        padding: 1rem;
    }
</style>
<div class="theme-container">
    <div class="theme-pattle" style="background: #3E4551;">
        <p style="color: white;">Default</p>
    </div>
    <div class="theme-pattle" style="background: #424242;">
        <p style="color: white;">Classic</p>
    </div>
    <div class="theme-pattle" style="background: #C62828;">
        <p style="color: white;">Cranberry</p>
    </div>
    <div class="theme-pattle" style="background: #ad1457;">
        <p style="color: white;">Byzantium</p>
    </div>
    <div class="theme-pattle" style="background: #6a1b9a;">
        <p style="color: white;">Orchids</p>
    </div>
    <div class="theme-pattle" style="background: #4527a0;">
        <p style="color: white;">Blueberry</p>
    </div>
    <div class="theme-pattle" style="background: #283593;">
        <p style="color: white;">Starrynights</p>
    </div>
    <div class="theme-pattle" style="background: #1565C0;">
        <p style="color: white;">Electric</p>
    </div>
    <div class="theme-pattle" style="background: #0277bd;">
        <p style="color: white;">Oceanic</p>
    </div>
    <div class="theme-pattle" style="background: #00695c;">
        <p style="color: white;">Emerald</p>
    </div>
    <div class="theme-pattle" style="background: #2E7D32;">
        <p style="color: white;">Aventurine</p>
    </div>
    <div class="theme-pattle" style="background: #ef6c00;">
        <p style="color: white;">Tropical</p>
    </div>
    <div class="theme-pattle" style="background: #d84315;">
        <p style="color: white;">Ginger</p>
    </div>
    <div class="theme-pattle" style="background: #4e342e;">
        <p style="color: white;">Espresso</p>
    </div>
    <div class="theme-pattle" style="background: #37474f;">
        <p style="color: white;">Enigma</p>
    </div>
</div>

## Usage

Open `.env`, add or modify the following:

```ini
APP_THEME=byzantium
```

!> You can pick any theme above, just remember using lower case or it wouldn't apply.