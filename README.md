# BeamAvatar Component

BeamAvatar is a customizable avatar component for Svelte, inspired by [Boring Avatars](https://github.com/boringdesigners/boring-avatars). It generates unique and consistent avatars based on usernames and custom color palettes.

## Installation

```bash
# Clone and copy BeamAvatar.svelte into your project
cp BeamAvatar.svelte src/components/
```

## Basic Usage

```svelte
<script>
  import BeamAvatar from './BeamAvatar.svelte';
</script>

<BeamAvatar name="John Doe" />
```

## Props

| Prop   | Type     | Default                                                 | Description                           |
| ------ | -------- | ------------------------------------------------------- | ------------------------------------- |
| name   | string   | 'Biricato'                                              | Text used to generate the avatar      |
| colors | string[] | ['#fe4365', '#fc9d9a', '#f9cdad', '#c8c8a9', '#83af9b'] | Array of 5 colors used for the avatar |
| size   | number   | 36                                                      | Size of the avatar in pixels          |
| square | boolean  | false                                                   | Whether to render a square avatar     |
| title  | string   | undefined                                               | Optional title attribute for the SVG  |

## Examples

### Basic Avatar
```svelte
<BeamAvatar name="John Doe" />
```

### Custom Size
```svelte
<BeamAvatar 
  name="John Doe" 
  size={80} 
/>
```

### Custom Colors
```svelte
<BeamAvatar 
  name="John Doe"
  colors={['#69d2e7', '#a7dbd8', '#e0e4cc', '#f38630', '#fa6900']}
/>
```

### Square Avatar
```svelte
<BeamAvatar 
  name="John Doe"
  square={true}
/>
```

### With Title
```svelte
<BeamAvatar 
  name="John Doe"
  title="Avatar for John Doe"
/>
```

## Credits

This component is inspired by [Boring Avatars](https://github.com/boringdesigners/boring-avatars) created by Hayk An, Javi Sánchez-Marín, Enric Pallerols and Josep Martins.

The default color palettes are from [Nice Color Palettes](https://github.com/Jam3/nice-color-palettes) by Matt DesLauriers.

## License

MIT License - Feel free to use this component in your projects.