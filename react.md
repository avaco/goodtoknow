# About React

It's a library not a framework

- Declarative UI for building interactive interfaces
- Component-based architecture
- Rich ecosystem and tooling
- Efficient updates with Virtual DOM
- Supported and maintained by Meta (Facebook)

## The Bad

- useEffect() (cloudflare dashboard bug)
- performance (useMemo, useCallback)
- infinite loops
- unnecessarily verbose
- referential stability
- Your input mysteriously clears itself? Turns out you switched a list item's key from a stable ID to an index, so React thinks it's a completely different component and remounts it, wiping state.
- you forgot that value can't be undefined? React saw it flip from uncontrolled to controlled and reset the input.
- You add a useEffect to fetch data, and suddenly your app is stuck in an infinite loop. The dependency array includes an object that gets recreated every render, so React thinks it changed and runs the effect again
  - Now you need useMemo and useCallback sprinkled everywhere to "stabilize identities," which is a thing you never had to think about before.
- Your click handler sees old state even though you just set it. That's a stale closure—the function captured the value from when it was created, and later renders don't magically update it.
  - You either need to put the state in the dependency array (creating a new handler every time) or use functional updates like setState(x => x + 1). Both solutions feel like workarounds.
- Debugging React requires understanding reconciliation algorithms, render phases, and how React's scheduler batches updates. 

"I've always find really funny how most of React docs, tutorials, discussions, ecc. are just about how not to use it and what other library/framework use on top of it to add even more layers of abstractions for doing basic things I could have done while trying to make sense of all this mess. This is beyond leaky abstraction, the concept of black-box was never taken into account while designing React, how can a new learner not feel overwhelmed by needing to know internal mechanisms just to do basic things that React should've allowed to do out-of-the-box without the need of knowing how the freaking re-render internal mechanism works, who cares. Where is the abstraction if I need to know about the internals to use the abstraction itself? Overengineering the front-end was the worst of all the choices, maybe frontenders are trying hard not to be replaced by AI by keeping on creating new overengineered frameworks. Let's make frontend simple again, your apps won't really scale that much, you don't really need all of that abstraction layers, you are just trying to justify your bad choices to yourself, please face the truth and embrace vanilla JS, CSS, HTML and a separate backend without any fancy API route/server function powered framework." --some comment on a react youtube video
