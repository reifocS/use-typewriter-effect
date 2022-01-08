# use-typewriter-effect

> Highly flexible React hook with declarative API for typewriting effect

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
## Typewriter API

In order to access the typewriter API, you must first call getTypewriter and pass it the typewriter hook dispatch.  
Rendering will start after the trigger method is called. This gives you full control over the typing sequence.
You can use it inside a useEffect or in event handlers.

### Options

| Name       | Type     | Default | Description                                    |
| ---------- | -------- | ------- | ---------------------------------------------- |
| type        | string   | null     | Write the given string. |
| pauseFor        | number   | null      | Pause the typing. |
| deleteSome  | number   | null    |  Delete some characters.        |
| deleteAll |    |     | Delete all typed characters so far.         |
| setLoop |  boolean  |     | If the given sequence of events should loop.           |
| setDelay |   number | [60:120]  | Typing speed (ms)        |
| trigger |    |     | Update typewriter state with the previously built sequence of events and start rendering        |


## License

MIT


