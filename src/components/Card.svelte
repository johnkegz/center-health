<script>
    export let currentData;
    export let average;
    export let percentage;
    export let prevData;
    export let prevAverage;
    export let prevPercentage;
</script>

<div class="cardContainer">
    <div class="card">
        <div class="container">
            <div class="card-header">
                <div class="card-icon" />
                <div class="card-title">Total blood suger events</div>
            </div>
            {#if currentData.length !== 0}
                <div class="card-body">
                    <div class="card-dot" />
                    <div class="card-body-number">{currentData.length}</div>
                    <div class="card-body-word">events</div>
                </div>
            {:else}
                <div class="card-body-none">Not enough data</div>
            {/if}
            <div class="card-footer">
                <div class="card-footer-word">Previous day</div>
                <div>
                    <span class="footer-sign">-</span>
                    {#if currentData.length !== 0}
                        <span class="card-footer-number">{prevData.length}</span
                        >
                    {/if}
                </div>
            </div>
        </div>
    </div>
    <div class="card">
        <div class="container">
            <div class="card-header">
                <div class="card-icon" />
                <div class="card-title">Average blood sugar</div>
            </div>
            {#if currentData.length !== 0}
                <div class="card-body">
                    
                    {#if average > prevAverage}
                    <div class="card-status-up" />
                    {:else}
                    <div class="card-status-drop" />
                    {/if}

                    <div class="card-body-number">{average}</div>

                    <div class="card-body-word">mg/dL</div>
                </div>
            {:else}
                <div class="card-body-none">Not enough data</div>
            {/if}
            <div class="card-footer">
                <div class="card-footer-word">Previous day</div>
                <div>
                    <span class="footer-sign">-</span>
                    {#if currentData.length !== 0}
                        <span class="card-footer-number-average">{prevAverage}</span>
                    {/if}
                </div>
            </div>
        </div>
    </div>
    <div class="card">
        <div class="container">
            <div class="card-header">
                <div class="card-icon" />
                <div class="card-title">Events between 70 and 180</div>
            </div>
            {#if currentData.length !== 0}
                <div class="card-body">
                    <div class="card-dot" />
                    <div class="card-body-number">{percentage}%</div>
                    <div class="card-body-word">events</div>
                </div>
            {:else}
                <div class="card-body-none">Not enough data</div>
            {/if}
            <div class="card-footer">
                <div class="card-footer-word">Previous day</div>
                <div>
                    <span class="footer-sign">-</span>
                    {#if currentData.length !== 0}
                        <span class="card-footer-number-percent">{prevPercentage}%</span
                        >
                    {/if}
                </div>
            </div>
        </div>
    </div>
</div>

<style>
    .cardContainer {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        grid-gap: 10px;
        margin-bottom: 10px;
    }

    .card {
        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
        transition: 0.1s;
        width: 100%;
        height: 115px;
        border-radius: 15px;
    }

    .card:hover {
        box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
    }

    .container {
        padding: 2px 16px;
    }

    .card-header {
        display: flex;
    }

    .card-icon {
        height: 23px;
        width: 20px;
        background: url("../images/event-sprite.png");
        background-size: 20px 130px;
        background-repeat: no-repeat;
        opacity: 0.5;
        background-position: 0 1px;
    }

    .card-title {
        opacity: 0.8;
        align-self: flex-end;
        padding-top: 4px;
    }

    .card-body {
        display: flex;
        justify-content: flex-end;
        opacity: 0.5;
    }

    .card-body-none {
        display: flex;
        justify-content: flex-end;
        opacity: 0.5;
        height: 40px;
        margin-top: 6px;
    }

    .card-dot {
        align-self: center;
        height: 5px;
        width: 5px;
        background-color: #0af;
        border-radius: 50%;
        margin-right: 10px;
    }

    .card-body-number {
        font-size: 35px;
        opacity: 0.5;
        align-self: center;
        margin-bottom: 0;
        margin-right: 2px;
    }

    .card-body-word {
        opacity: 0.5;
        align-self: flex-end;
        padding-bottom: 8px;
    }

    .card-footer {
        display: flex;
        justify-content: flex-end;
    }

    .card-footer-word {
        opacity: 0.5;
        margin-right: 2px;
    }

    .card-footer-number {
        color: #0af;
    }

    .card-footer-number-average {
        color: orange;
    }

    .card-footer-number-percent {
        color: green;
    }

    .footer-sign {
        opacity: 0.5;
    }

    .card-status-drop {
        height: 28px;
        width: 20px;
        background: url("../images/status-sprite.png");
        background-size: 80px 45px;
        background-repeat: no-repeat;
        align-self: center;
        background-position: 0 -25px;
    }

    .card-status-up {
        height: 22px;
        width: 20px;
        background: url("../images/status-sprite.png");
        background-size: 80px 41px;
        background-repeat: no-repeat;
        background-position: 0 1px;
        align-self: center;
        margin-bottom: 8px;
    }

    @media (max-width: 1156px) {
		.cardContainer {
        grid-template-columns: 1fr 1fr;
        }
	}

    @media (max-width: 540px) {
        .cardContainer {
            grid-template-columns: 1fr 1fr;
        }
    }

    @media (max-width: 414px) {
        .cardContainer {
            grid-template-columns: 1fr;
        }
    }
</style>
