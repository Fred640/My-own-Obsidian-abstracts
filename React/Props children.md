Чтобы добавлять аргументы и props из вне в компонент используеться props children

```
function MyButton ({children, ...props}) {
    return(
        <button {...props} className={classes.myBtn}>
            {children}
        </button>
    )
}
```

```
<MyButton disbled>Ватафак</MyButton>
```