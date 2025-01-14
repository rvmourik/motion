# useMotionProperties

useMotionProperties is used to access [**Motion Properties**](/motion-properties) for a target element.

Motion properties are combining [**useElementStyle**](/api/use-element-style) and [**useElementTransform**](/api/use-element-transform).

It allows to add another **layer** between **variants** and direct element **styling**, and a **cleaner** data format from [**variants**](/variants).

## Parameters

### `target`

Target must be an element (**SVG** / **HTML**), or a reference to an element.

If the target **reference** is **updated**, the **current** motion properties will be **updated** from the new **element** styling.

## Exposed

### `motionProperties`

Motion properties are an object combining [**Style Properties**](/motion-properties#style-properties) and [**Transform Properties**](/motion-properties#transform-properties).

Change a **value** and it will be **updated** on the target **element**.

### `style`

A style property from [**useElementStyle**](/api/use-element-style).

### `transform`

A style property from [**useElementTransform**](/api/use-element-transform).

## Example

```typescript
const target = ref<HTMLElement>()

const { motionProperties } = useMotionProperties(target)

motionProperties.opacity = 0

motionProperties.scale = 2
```
