<script>
    import Theme from './Theme.svelte'
</script>

<style>
    * {
        color: var(--basic-font-color);
    }

    nav {
        display: flex;
        justify-content: space-between;
    }
</style>

<nav>
    <h1 class="mono">GithubFinder</h1>

    <Theme />
</nav>