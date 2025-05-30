---
title: StateHistory
description: Track state changes with undo/redo capabilities
category: State
---

<script>
import Demo from '$lib/components/demos/state-history.svelte';
</script>

## Demo

<Demo />

## Usage

`StateHistory` tracks a getter's return value, logging each change into an array. A setter is also
required to use the `undo` and `redo` functions.

<!-- prettier-ignore -->
```ts
import { StateHistory } from "runed";

let count = $state(0);
const history = new StateHistory(() => count, (c) => (count = c));
history.log[0]; // { snapshot: 0, timestamp: ... }
```

Besides `log`, the returned object contains `undo` and `redo` functionality.

<!-- prettier-ignore -->
```svelte
<script lang="ts">
	import { StateHistory } from "runed";

	let count = $state(0);
	const history = new StateHistory(() => count, (c) => (count = c));
</script>

<p>{count}</p>

<button onclick={() => count++}>Increment</button>
<button onclick={() => count--}>Decrement</button>

<button disabled={!history.canUndo} onclick={history.undo}>Undo</button>
<button disabled={!history.canRedo} onclick={history.redo}>Redo</button>
```
