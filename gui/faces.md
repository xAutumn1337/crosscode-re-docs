
# Location 

`assets/data/characters/*/*.json`


# When is it seen in game?

Faces are usually seen during cutscenes. They are the character expressions that are accompanied by the text.

# Format

```
{
    "face" : {
        "subImages" : {},
        "width" : int,
        "height" : int,
        "centerX" : int,
        "centerY" : int,
        "src" : "src.png",
        "parts" : [],  
        "expressions" : {}
    }
}
```


# Face 
| **Key** | **type** | **Info** |
|-----| ----- | ------|
| `subImages` | [SubImage](#subimage) | ??? |
| `width` | [int](#integer) | How wide the reference image is |
| `height` | [int](#integer)| How tall the reference image is |
| | | |
| `centerX` | [int](#integer) | Center of face x-coordinate |
|           |                 | To calculate you do|
|           |                 | 28px  + pixel translation from PartConfig.srcX |
|           |                 | The size of the Part display in the pause menu|
|           |                 | is a fixed 56px (roughly 10% of the internal screen width)|
| | | |
| `centerY` | [int](#integer) | Center of face y-coordinate  |
|           |                 | To calculate you do|
|           |                 | 21px  + pixel translation from PartConfig.srcY |
|           |                 | The size of the Part display in the pause menu|
|           |                 | is a fixed minimum 42px |
|           |                 | The height is as big as the text is |
| | | |
| `src`     | [Image Path](#img-loc) | default source image to use |
| `parts`   | [parts](#parts) | ??? | 
| `expression` | [expression](#expression) | ??? |


# Types

## <a id="integer">Integer</a>

A number 

---
---
---

## <a id="float">Float</a>

A number with a decimal.

---
---
---

## <a id="string">String</a>

A series of characters 

---
---
---

## <a id="subimage">SubImage</a>
```js
{
    "name" : "value"
}
```
| **key** | **type** | **info** |
| ------- | -------- | -------- |
|  `name`   |  [str](#string)     |  The name of the subImage (must be unique) |
|  `value`  |  [Image Path](#img-loc)     | ??? | 


---

## <a id="img-loc">Image Location</a>

`assets/media/face/*/*.png`

---
---
---
## <a id="parts">parts</a>

```js
{
    "parts" : [Part]
}
```

| **key** | **type** | **info** |
| ------- | -------- | -------- |
| `Part`  | [Part](#part)     | Array of body parts |

---

## <a id="part">Part</a>
```js
{
    "name" : PartConfig,
     ...
    "nameN" : PartConfig
}
```

| **key** | **type** | **info** |
| ------- | -------- | -------- |
| `name`  | [str](#string) | Body part name (unique) |
| `PartConfig` | [PartConfig](#part-config) | ??? |

---


## <a id="part-config">PartConfig</a>

```js
{
    "destX" : int,
    "destY" : int,
    "subX"  : int,
    "subY"  : int,
    "width" : int,
    "height": int,
    "srcX"  : int,
    "srcY"  : int,
    "img"   : str    
}
```

| **key** | **type** | **info** |
| ------- | -------- | -------- |
|  `destX` | [int](#integer) | In game destination X-coord |
|  `destY` | [int](#integer) | In game destination Y-coord |
|  `width` | [int](#integer) | Width of body part in the image file|
|  `height`| [int](#integer) | Height of body part in the image file  |
|  `srcX`  | [int](#integer) | X-coordinate location in image file |
|  `srcY`  | [int](#integer) | Y-coordinate location in image file |

**OPTIONAL** 

| **key** | **type** | **info** |
| ------- | -------- | -------- | 
| `subX`  | [int](#integer)  | destX adjustment value |
| `subY`  | [int](#integer)  | destY adjustment value|
| `img`   | [str](#string)  | SubImage to use (key name) |

*Note: subX and subY are carried over to the remaining parts, but skips the current one.
 ---
---
---
## <a id="expression">expression</a>
```js
{
    "name" : ExpressionConfig,
}
```

| key    | type  | info |
|--------|-------|------|
| name   | [str](#string) | Name of the expression |
| value  | [ExpressionConfig](#expression-config) | ??? |
---

## <a id="expression-config">ExpressionConfig</a>
```js
[{
    "anim" : [int],
    "time" : float,
    "repeat": int,
    "faces" : [Face]         
}]
```

| key    | type  | info |
|--------|-------|------|
| faces  | [Array#Face](#face-array)  | ??? |

**OPTIONAL** 

| **key** | **type** | **info** |
| ------- | -------- | -------- | 
| anim   | [Array#int](#integer) | Each array value is a face frame to play  |
| time   | [float](#float) | Time between each new frame (anim required) |
| repeat | [int](#integer)   | behavior of value n detailed below (anim required) |
|        |       | n >= anim.length - Game crashes | 
|        |       | n > 1 - At what frame to loop back to infinitely |
|        |       | n == 0 - Only play once |
|        |       | (n < 0 or n == 1) - infinitely loop full animation |

 ---

 ## <a id="face-array">Face</a>
 ```
[
    str,
    ...
    str
]
```
| key    | type  | info |
|--------|-------|------|
| index  | [int](#integer)   | Not an explict key. Corresponds to which part it's from. |
| value  | [str](#string)   | Name of part.|

---
---
---


# EXTRAS

The faces reference point is at 192px on the y-axis.

The x-axis is more variable and depends on which side its on.

One person only:
LEFT is 32px.

RIGHT is 408px.

*Note: Assumes screen dimensions are 568px by 320px.

 
