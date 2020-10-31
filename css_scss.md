

```scss
.container{
    padding: 3em;
    display: grid;
    grid-gap: 2em;

    .quote{
        padding: 2em;
        border-radius: .3em;
        box-shadow: 10px 10px 30px rgba(0, 0, 0, 0.1);
    }

    p{
        margin-top: 0;
    }

    span {
        font-weight: bold;
        position: relative;
        margin-left: 15px;

        &:before {
            content: '';
            position: absolute;
            height: 1px;
            width: 10px;
            border-bottom: 1px solid black;
            top: 10px;
            left: -15px;

        }
    }
}
```