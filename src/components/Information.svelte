<script>
    import Social from './Social.svelte'
    import { username } from '../store.js'

    $: $username, changed()
    
    let fetchData = (async () => {
        const response = await fetch(`https://api.github.com/users/${ $username }`)
        const res = await response.json()
        const date = new Date(res.created_at.substr(0, 10))
        res.joined_at = date.toString().substr(4, 11)

        return res
    })()

    const changed = () => {
        fetchData = (async () => {
            const response = await fetch(`https://api.github.com/users/${ $username }`)
            const res = await response.json()
            const date = new Date(res.created_at.substr(0, 10))
            res.joined_at = date.toString().substr(4, 11)
    
            return res
        })()
    }
</script>

<style>
    .information {
        width: 100%;
        display: flex;
        background: var(--card-bg);
        padding: 50px;
        margin-top: 20px;
        border-radius: 10px;
    }
    
    .information * {
        color: #fff;
    }

    .information img {
        border-radius: 50%;
        width: 100px;
        height: 100px;
        object-fit: cover;
    }

    .information .data {
        margin-left: 20px;
        width: 100%;
    }

    .information .top {
        display: flex;
        align-items: center;
        justify-content: space-between;
        width: 100%;
        padding-top: 50px;
        position: relative;
    }

    .information .top div h2 {
        color: var(--basic-font-color);
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
        width: 65%;
        position: absolute;
        margin-top: -60px;
    }

    .information .top .date {
        color: #8991ac;
        font-size: 10px;
        position: absolute;
        right: 0;
        top: 0;
    }

    .information .username {
        color: #1253a2;
        text-decoration: none;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
        width: 60%;
        position: absolute;
        margin-top: -25px;
    }

    .information .data .bio {
        margin-top: 10px;
        margin-bottom: 15px;
        color: #8991ac;
    }

    .information .data .numbers-chart {
        width: 100%;
        background: var(--numbers-chart-bg);
        padding: 20px;
        margin-top: 30px;
        border-radius: 10px;
        display: grid;
        grid-template-columns: repeat(3, 1fr);
    }

    .information .data .numbers-chart .item .name {
        font-size: 15px;
        color: #7a8190;
    }

    .information .data .numbers-chart .item .number {
        font-size: 25px;
        font-weight: bold;
        margin-top: 5px;
        color: var(--basic-font-color);
    }

    @media(max-width: 750px) {
        .information {
            padding: 30px;
            flex-direction: column;
            position: relative;
        }

        .information .top {
            flex-direction: column;
            justify-content: flex-end;
            align-items: flex-end;
            position: absolute;
            top: 30px;
            right: 30px;
        }

        .information .top div {
            display: flex;
            justify-content: flex-end;
            align-items: flex-end;
            flex-direction: column;
        }

        .information .top .date {
            margin-top: 10px;
        }

        .information .data {
            margin-left: 0;
            margin-top: 10px;
        }

        .information .top div h2 {
            right: 0;
            width: 50%;
            top: 80px;
        }
        
        .information .top div a {
            right: 0;
            width: 45%;
            top: 80px;
        } 
    }
    
    @media(max-width: 475px) {
        .information img {
            width: 75px;
            height: 75px;
        }

        .information .top div h2 {
            right: 0;
            width: 40%;
            top: 80px;
        }
        
        .information .top div a {
            right: 0;
            width: 35%;
            top: 80px;
        } 
        
    }
</style>


{#await fetchData}
    <div class="information">
        <p>Loading...</p>
    </div>
{:then data}
    <div class="information">
        <img src={ data.avatar_url } alt="Profile">

        <div class="data">
            <div class="top">
                <div>
                    <h2 class="mono">{ data.name ? data.name : data.login }</h2>
                    <a href={ data.html_url } class="username mono" target="_blank">@{ data.login }</a>
                </div>
                
                <p class="date mono">Joined { data.joined_at }</p>
            </div>


            <div class="bio mono" style={ data.bio ? 'color: var(--basic-font-color);' : '' } >{ data.bio ? data.bio : 'This profile has no bio' }</div>

            <div class="numbers-chart">
                <div class="item">
                    <div class="name">Repos</div>
                    <div class="number">{ data.public_repos }</div>
                </div>
                <div class="item">
                    <div class="name">Followers</div>
                    <div class="number">{ data.followers }</div>
                </div>
                <div class="item">
                    <div class="name">Following</div>
                    <div class="number">{ data.following }</div>
                </div>
            </div>

            <Social { data } />
        </div>
    </div>
{:catch error}
    <div class="information" style="color: var(--basic-font-color);">
       @{ $username } does not exist!
    </div>
{/await}

