```
// trouble shooting //
 1. goal : prevent multiple comment components open
 2. tried but failed :
    from parent component, pass useRef or useState to children.
    they will store functions that close comment in its component.
    but type(it means type-script) for them is very difficult,
    when clicked the "답글", first set false all the comment component, but it didn't work,
    and in the process, things work unexpectedly
     - in useEffect, ref.current, the idea itself - and it occured - multiple useState in one ref or state, so on...
 3. solved : to use global client state.
    first clicked "답글", get the function to close comment and set global state
    second clicked other "답글", use the function to close comment.
    that's it! // I got this over half day long struggled....
 4. ps : well, although there is better UI design, something important is go to next step - making next page..
    detail will be set later. (and from now, I have changed various things that I had worked hard...)
    many things is best at that time, but time is gone, it is not...
```



https://user-images.githubusercontent.com/60069112/160235979-a34a214a-676d-4304-9e28-edd470f2cf29.mp4


https://user-images.githubusercontent.com/60069112/160235982-27943c72-892d-4760-b500-2b851a3e017f.mp4

-22.03.26-
