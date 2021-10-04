<div class="nav-bar">
    <div class="logo">
        <img
            src={"images/logo.png"}
            width="50px"
            height="50px"
            alt="center health"
        />
    </div>
    <div class="verticalLine" />
    <div class="page">Dashboard</div>
</div>

<style>
    .nav-bar {
        width: 100%;
        /* padding-left: 15px; */
        height: auto;
        display: flex;
        background-image: linear-gradient(to bottom, #0af, #acfffd 120px);
    }

    .logo {
        padding: 0.6rem;
    }

    .verticalLine {
        width: 1px;
        margin: 0.6rem;
        height: 35px;
        background-color: #ffffff;
        align-self: center;
        opacity: 0.4;
    }

    .page {
        padding: 0.6rem;
        align-self: center;
        color: #ffffff;
        font-size: 32px;
        letter-spacing: 1px;
    }

    @media (max-width: 540px) {
		.nav-bar {
            padding-left: 0px;
    }
	}
</style>
