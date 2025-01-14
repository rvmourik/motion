# Motion Instance

Motion instance is the **object** exposed when **binding** to a target **element** using [**v-motion**](/directive-usage) or [**useMotion**](/composable-usage).

It is composed of **three properties**, allowing you to **interact** with the **element**.

## Variant

The variant is a **string reference**, that you can **modify** and **watch**.

It represents the **current variant** name of the **element**.

By modifying this **variant**, you will trigger a **transition** between the **current** variant and the one you just **set**.

```vue
<script setup lang="ts">
// Define target.
const target = ref<HTMLElement>()

// Get the variant from target motion instance.
const { variant } = useMotion(target, {
  initial: {
    scale: 1,
    opacity: 0,
  },
  enter: {
    opacity: 1,
    transition: {
      // This will go to `custom` when enter is complete.
      onComplete: () => (variant.value = 'custom'),
    },
  },
  custom: {
    scale: 2,
    transition: {
      type: spring,
      damping: 100,
    },
  },
})
</script>
```

##### _Call customEvent to enable the custom variant_ ☝️

## Apply

Apply is a **function** that lets you **animate** to a **variant** definition, **without changing** the current **variant**.

This is useful when used with **event listeners**, or any **temporary** modification to the **motion** properties of the **element**.

This is also useful for **orchestration**, as **apply** returns a **promise**, you can await it and **chain** variant **applying**.

Apply **accepts** both a [**Variant Declaration**](/variants) or a **key** from the motion instance **variants**.

```vue
<script setup lang="ts">
// Define target.
const target = ref<HTMLElement>()

// Get the variant from target motion instance.
const { apply } = useMotion(target, {
  initial: {
    scale: 1,
    opacity: 0,
  },
  enter: {
    opacity: 1,
    scale: 1,
  },
})

const customEvent = async () => {
  // Animate to a temporary variant.
  await apply({
    scale: 2,
    transition: {
      type: spring,
      damping: 100,
    },
  })

  // Revert back to enter state
  await apply('enter')
}
</script>
```

##### _Call customEvent to Zboing the element_ ☝️

## Stop

Stop is a **function** that lets you **stop** ongoing **animations** for a specific **element**.

Calling it **without** argument will be stopping **all** the **animations**.

Calling it with an **array** of [**Motion Properties**](/motion-properties) keys will stop **every** specified **key**.

Calling it with a **single** motion property key will stop the specified **key**.

```vue
<script setup lang="ts">
// Define target.
const target = ref<HTMLElement>()

// Get the variant from target motion instance.
const { stop } = useMotion(target, {
  initial: {
    scale: 1,
    opacity: 0,
  },
  visible: {
    opacity: 1,
  },
})

const customEvent = () => {
  // Stop the current animations.
  stop()
}
</script>
```

##### _Call customEvent to stop the animations_ ☝️
