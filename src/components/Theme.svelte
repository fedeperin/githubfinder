<script>
    let root = document.documentElement
    let theme = localStorage.getItem('theme') ? localStorage.getItem('theme') : 'light'
    
    const lightTheme = () => {
        root.style.setProperty('--background', '#141c2f')
        root.style.setProperty('--basic-font-color', '#fff')
        root.style.setProperty('--card-bg', '#1f2a48')
        root.style.setProperty('--numbers-chart-bg', '#141c2f')
    }
    
    const darkTheme = () => {
        root.style.setProperty('--background', '#f5f8ff')
        root.style.setProperty('--basic-font-color', '#000')
        root.style.setProperty('--card-bg', '#fefefe')
        root.style.setProperty('--numbers-chart-bg', '#f5f8ff')
    }

    if(theme == 'dark') {
        darkTheme()
    }else {
        lightTheme()
    }
    const changeTheme = () => {
        if(theme == 'dark') {
            theme = 'light'
            lightTheme()
        }else {
            theme = 'dark'
            darkTheme()
        }

        localStorage.setItem('theme', theme)
    }

</script>

<style>
    * {
        color: var(--basic-font-color);
    }

    .theme {
        cursor: pointer;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .theme p {
        font-size: 15px;
        pointer-events: none;
    }

    .theme i {
        margin-left: 10px;
        font-size: 20px;
    }
</style>

{#if theme == 'dark'}
    <div class="theme" on:click={ changeTheme } >
        <p class="mono">DARK</p>
        <i class='bx bxs-moon'></i>
    </div>
{:else}
    <div class="theme" on:click={ changeTheme } >
        <p class="mono">LIGHT</p>
        <i class='bx bxs-sun'></i>
    </div>
{/if}