# Keyboard controls

Gebruik `window.addEventListener("keydown")` om te reageren op keyboard events in het window.

We gebruiken snelheid variabelen (`xspeed, yspeed`) om in de vier richtingen (Cursor keys of WASD) te bewegen.


```typescript
import * as PIXI from "pixi.js"

export class Ship extends PIXI.Sprite {
    xspeed = 0
    yspeed = 0

    constructor(texture: PIXI.Texture) {
        super(texture)

        window.addEventListener("keydown", (e: KeyboardEvent) => this.onKeyDown(e))
        window.addEventListener("keyup", (e: KeyboardEvent) => this.onKeyUp(e))
    }
    
    update() {
        this.x += this.xspeed
        this.y += this.yspeed
    }

    shoot(){
        console.log("shooooot!")
    }

    onKeyDown(e: KeyboardEvent): void {
        switch (e.key.toUpperCase()) {
            case " ":
                this.shoot()
                break;
            case "A":
            case "ARROWLEFT":
                this.xspeed = -7
                break
            case "D":
            case "ARROWRIGHT":
                this.xspeed = 7
                break
            case "W":
            case "ARROWUP":
                this.yspeed = -7
                break
            case "S":
            case "ARROWDOWN":
                this.yspeed = 7
                break
        }
    }

    private onKeyUp(e: KeyboardEvent): void {
        switch (e.key.toUpperCase()) {
            case " ":
                break;
            case "A":
            case "D":
            case "ARROWLEFT":
            case "ARROWRIGHT":
                this.xspeed = 0
                break
            case "W":
            case "S":
            case "ARROWUP":
            case "ARROWDOWN":
                this.yspeed = 0
                break
        }
    }
}

```

<br>
<br>
<Br>

## Sprite omdraaien
    
Als je karakter naar links beweegt wil je vaak de sprite omdraaien. Dit kan je doen door de `x scale` negatief te maken op het moment dat de arrow left of A knop wordt ingedrukt. Maak de scale weer positief als iemand op de arrow right of D knop drukt.
    
```typescript
this.scale.set(-1,1)
```

<br>
<br>
<Br>

## Stoppen met luisteren naar events

Als je een eventlistener aan het `window` toevoegt blijft die listener voor altijd actief. Het is dus belangrijk om met `removeEventListener()` de listener weer te verwijderen als de input niet meer nodig is.

Je moet hiervoor een extra variabele aanmaken van het type `EventListener`. Deze kan je vervolgens toevoegen en verwijderen:

```typescript
class App {

    mylistener:EventListener

    constructor(){
        this.mylistener = (e:Event) => this.logMessage(e)
        window.addEventListener('click', this.mylistener)
    }

    logMessage(e:Event){
        console.log("click event was called, now removing the listener!")
        window.removeEventListener("click", this.mylistener)
    }
}
```

<Br>
<br>
<Br>

## 🎮 Gamepad aansluiten

De webbrowser ondersteunt bluetooth gamepads, inclusief die van de Playstation en XBox. Lees [deze tutorial](https://developer.mozilla.org/en-US/docs/Web/API/Gamepad_API) voor het aansluiten van een gamepad!
    
<br>
<br>
<Br>
    
## Arcade stick controls
    
Bekijk [deze tutorial](https://github.com/HR-CMGT/PRG04-2021-2022-controller) voor het aansluiten van een arcade stick voor de CMGT Arcade kast.
