CSS можно применить к компоненту простым путем

```
function PostItem (props) {
    return (
        <div className="post">
            <div className="Post__content">
                <strong>{props.post.id} {props.post.title}</strong>
                <div>{props.post.body}</div>
                <button>Удалить</button>
            </div>
        </div>
    )
}
```

```
#root {
    display: flex;
    justify-content: center;
}

.App {
    width: 800px;
}

.post {
    display: flex;
    padding: 15px;
    border: 2px solid lightgreen;
    margin-top: 15px;
    justify-content: space-between;
    align-items: center;
}
```

Но место этого можно их изолировать и создать отдельный CSS файл для 1 компонента вот так:

```
import React from "react";
import classes from "./MyButton.module.css"
function MyButton (props) {
    return(
        <button className={classes.myBtn}>
            {props.children}
        </button>
    )
}
```

```
.myBtn {
    padding: 5px 15px;
    color: chartreuse;
    font-size: 14px;
    background: transparent;
    border: 1px solid rgb(46, 175, 46);
    cursor: pointer;
}

```