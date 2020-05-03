<script>
  export let type = "primary";
  export let flat = false;
  export let inverse = false;

</script>
<button class={type} class:flat={flat} class:inverse={inverse} on:click>
<slot></slot>
</button>
<style>
button {
    text-shadow: none;
    background-image: none;
    cursor: pointer;
    display: inline-block;
    outline: none;
    border:none;
    font-weight: 700;
    text-align: center;
    text-decoration: none;
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0,0,0,.2);
    padding: 11px 21px;
}
.primary {
    background-color: #d91b42;
    color: #fff;
}
.primary:focus {
    background: #d91b42;
}
.secondary {
    background-color: #6435c9;
    color: #fff;
}
.secondary:focus {
    background-color: #6435c9;
}
.success {
    background-color: #21ba45;
    color: #fff;
}
.success:focus {
    background-color: #21ba45;
}
.flat {
    box-shadow: none;
}
.primary.inverse {
    color: #d91b42;
    background: #fff;
    border: 1px solid #d91b42;
}
.secondary.inverse {
    color: #6435c9;
    background: #fff;
    border: 1px solid #6435c9;
}
.success.inverse {
    color: #21ba45;
    background: #fff;
    border: 1px solid #21ba45;
}
</style>