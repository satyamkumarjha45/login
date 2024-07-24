<script>
    import { Route } from "tinro";
    import Login from "./routes/Login.svelte";
    import Register from "./routes/Register.svelte";
    import ToDoList from "./routes/ToDoList.svelte";
</script>

<Route path="/"><Login /></Route>
<Route path="/register"><Register /></Route>
<Route path="/todo"><ToDoList /></Route>

<style>
    /* Your global styles */
</style>
