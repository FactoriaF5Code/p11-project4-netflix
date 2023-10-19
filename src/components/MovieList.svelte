<script>
    import { onMount } from "svelte";

    const url =
        "https://api.themoviedb.org/3/discover/movie?include_adult=false&include_video=false&language=ca&page=1&sort_by=popularity.desc";
    const options = {
        method: "GET",
        headers: {
            accept: "application/json",
            Authorization:
                "Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI3ZjY1ZjUyYTFhZjEzZGE3MGM5NmE3YThkNWFiY2QxMiIsInN1YiI6IjY1MmViMjNkMDI0ZWM4MDBhZWNkODQ3YyIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.xm2vMk77fgNrHeY_Owril1M3vhViD3rY6Tx7LSvaiz0",
        },
    };

    let movies = [];

    onMount(() =>
        fetch(url, options)
            .then((response) => response.json())
            .then((data) => (movies = data.results))
            .catch((err) => console.error(err))
    );
</script>

<div>
    {#each movies as movie}
        <img
            alt="Cover"
            src={`https://image.tmdb.org/t/p/original/${movie.poster_path}`}
        />
    {/each}
</div>

<style>
    div {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 15px;
    }
    img {
        height: 151px;
        width: 275px;
        object-fit: cover;
    }
</style>
