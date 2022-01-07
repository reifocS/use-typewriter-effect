# use-typewriter-effect

> Highly flexible React hook for typewriting effect

## Install

```bash
npm install --save use-typewriter-effect
```
## Demo
https://vincent-escoffier.vercel.app/typewriter

## Basic Usage

```tsx
import React from "react";
import useTypewriterEffect, {
  getTypewriter,
  useCursor,
} from "use-typewriter-effect";

function App() {
  const [state, dispatch, isTyping] = useTypewriterEffect();
  const cursor = useCursor(isTyping);

  React.useEffect(() => {
    getTypewriter(dispatch)
      .type("Hello world!")
      .pauseFor(1000)
      .deleteSome("6")
      .type("universe!")
      .pauseFor(1000)
      .deleteAll()
      .setLoop(true)
      .trigger();
      
      // React guaranties that dispatch reference is stable, so we can safely
      // declare it as a dependency
  }, [dispatch]);

  return (
    <main>
      <p>
        {state}
        <span style={{ visibility: cursor ? "visible" : "hidden" }}>|</span>
      </p>
    </main>
  );
}
```
## Example from the demo
```tsx
import React from "react";
import useTypewriterEffect, {
    getTypewriter,
    useCursor,
} from "use-typewriter-effect";

function App() {
    const [state, dispatch, isTyping] = useTypewriterEffect();
    const cursor = useCursor(isTyping);

    React.useEffect(() => {
        getTypewriter(dispatch)
            .type("Hello world!\n How are you")
            .pauseFor(1000)
            .deleteAll()
            .type("This is a typewriter effect")
            .pauseFor(1000)
            .deleteSome(6)
            .type("hook!")
            .pauseFor(1000)
            .deleteAll()
            .setLoop(true)
            .trigger()
    }, [dispatch]);

    const sentences = state.split("\n");
    const lastSentence = sentences.pop();
    return (
        <main>
            <input type="text" placeholder={lastSentence}/>

            <div>
                {sentences.map((sen, i) => (
                    <p key={i}><span style={{color:"cyan"}}>$</span> {sen}</p>
                ))}
                <p>
                    <span style={{color:"cyan"}}>$</span> {lastSentence}
                    <span style={{visibility: cursor ? "visible" : "hidden"}}>|</span>
                </p>
            </div>
        </main>
    );
}


```
## License

MIT


