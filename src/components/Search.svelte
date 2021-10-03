<script>
    import { username } from '../store.js'
    let input

    const submitForm = () => {
        if(input.trim() !== '') {
            username.set(input)
        }
        
        input = ''
    }
</script>

<style>
    .search {
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: center;
        background: var(--card-bg);
        padding: 30px;
        margin-top: 20px;
        border-radius: 10px;
    }
    
    .search * {
        color: #fff;
        transition: all .5s ease;
    }
    
    .search input {
        width: 100%;
        background: var(--card-bg);
        border: none;
        outline: none;
        padding: 0 10px;
        font-size: 30px;
        margin-bottom: 5px;
        color: var(--basic-font-color);
    }
    
    .search input::placeholder {
        color: #98a0b7;
        font-size: 20px;
    }
    
    .search i {
        color: #2a5c9e;
        font-size: 40px;
        cursor: pointer;
    }
    
    .search i:hover {
        color: #1e73e2;
    }

    .search button {
        font-size: 20px;
        padding: 10px;
        background: #0278fc;
        cursor: pointer;
        outline: none;
        border: none;
        border-radius: 10px;
    }

    .search button:hover {
        opacity: 0.7;
    }
</style>

<form class="search" on:submit|preventDefault={ submitForm } >
    <label for="search">
        <i class='bx bx-search'></i>
    </label>
    <input type="text" placeholder="Search GitHub username..." name="search" id="search" autocomplete="off" class="mono" bind:value={ input }>

    <button class="mono">Search</button>
</form>