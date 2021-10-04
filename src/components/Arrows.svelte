<script>
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();

    const nextdate = () => dispatch("nextdate");

    const prevdate = () => dispatch("prevdate");
</script>

<div class="nav-bar">
    <div class="logo">
        <div class="icon icon-1" on:click={prevdate} />
        <div class="icon icon-2" on:click={nextdate} />
    </div>
</div>

<style>
    .logo {
        display: flex;
    }

    .icon {
        height: 15px;
        width: 15px;
        background: url("../images/arrow-sprite.png");
        background-size: 15px 60px;
        background-repeat: no-repeat;
        opacity: 0.5;
        
    }

    .icon-1 {
        background-position: 0 -45px;
    }

    .icon-2 {
        background-position: 0 -15px;
        margin-left: 35px;
    }

    .icon:hover {
        background-color: rgba(0,0,0,.5);
        cursor: pointer;
        border-radius: 50px;
        size: 10px;
    }
</style>
