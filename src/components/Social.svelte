<script>
    export let data
</script>

<style>
    .social {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        grid-gap: 10px;
        margin-top: 20px;
        width: 100%;
    }

    .social .social-item {
        width: 100%;
        display: flex;
        align-items: center;
        position: relative;
    }
    
    .social .social-item p, .social .social-item a {
        margin-left: 35px;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
        width: 75%;
        position: absolute;
    }
    
    .social .social-item i {
        font-size: 30px;
    }
    
    .social-item * {
        color: var(--basic-font-color);
    }

    .social-item.gray * {
        color: gray;
    }

    @media(max-width: 700px) {
        .social {
            grid-template-columns: 1fr;
        }

    }
</style>

<div class="social">
    {#if data.location !== null}
        <div class="social-item">
            <i class='bx bxs-map'></i>
            <p>{ data.location }</p>
        </div>
    {:else}
        <div class="social-item gray">
            <i class='bx bxs-map'></i>
            <p>Not Available</p>
        </div>
    {/if}

    {#if data.twitter_username !== null}
        <div class="social-item">
            <i class='bx bxl-twitter'></i>
            <p>{ data.twitter_username }</p>
        </div>
    {:else}
        <div class="social-item gray">
            <i class='bx bxl-twitter'></i>
            <p>Not Available</p>
        </div>
    {/if}

    {#if data.blog !== ''}
        <div class="social-item">
            <i class='bx bx-link'></i>
            <a href={ data.blog } target="_blank">{ data.blog }</a>
        </div>
    {:else}
        <div class="social-item gray">
            <i class='bx bx-link'></i>
            <p>Not Available</p>
        </div>
    {/if}

    {#if data.company !== null}
        <div class="social-item">
            <i class='bx bxs-city'></i>
            <p>{ data.company }</p>
        </div>
    {:else}
        <div class="social-item gray">
            <i class='bx bxs-city'></i>
            <p>Not Available</p>
        </div>
    {/if}
</div>