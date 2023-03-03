<template>
    <div class="stopwatch">
        <p class="stopwatch__add-counts">
            Mins:
            <input
                v-model="minutes"
                type="number"
                value="0"
                min="0"
                max="60"
            >
            Secs:
            <input
                v-model="seconds"
                type="number"
                value="0"
                min="0"
                max="60"
                step=10
            >
        </p>
        <div
            class="stopwatch__time"
            :class="{'stopwatch__time-active': isActive}"
        >
            <p>
                {{ stopwatchTime + endTime }}
            </p>
        </div>
        <div class="stopwatch__btns">
            <button
                v-if="!isActive"
                class="btnsvg btn-left"
                @click="run"
            >
                <svg class="svg" width="17" height="20" viewBox="0 0 17 20" xmlns="http://www.w3.org/2000/svg">
                    <path d="M0 20V0L17 10L0 20Z"/>
                </svg>
            </button>
            <button
                v-else
                class="btnsvg btn-left"
                @click="fix"
            >
                <svg class="svg" width="10" height="20" viewBox="0 0 10 20"  xmlns="http://www.w3.org/2000/svg">
                    <rect x="7" width="3" height="20" />
                    <rect width="3" height="20" />
                </svg>
            </button>
            <button
                class="btnsvg btn-rigth"
                @click="reset"
            >
                <svg class="svg" width="20" height="20" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                    <rect width="20" height="20"/>
                </svg>
            </button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'theStopwatch',
    data() {
        return {
            deadline: null,
            minutes: 0,
            seconds: 0,
            elapsedTime: null,
            requestAnimationId: null,
            isActive: false,
            endTime: '',
        };
    },
    computed: {
        stopwatchTime() {
            if (this.elapsedTime) {
                const seconds = this.elapsedTime.getUTCSeconds().toString();
                const minutes = this.elapsedTime.getUTCMinutes().toString();
                const miliseconds = this.elapsedTime.getMilliseconds().toString();

                let result = (minutes < 10 ? '0' + minutes : minutes) + ':';
                result += (seconds < 10 ? '0' + seconds : seconds) + ':'
                result += (miliseconds < 100 
                    ? '0' + miliseconds
                    : miliseconds < 10 ? '00' + miliseconds : miliseconds);

                return result;
            }

            return '00.00.000';
        },
    },
    methods: {
        tick() {
            this.elapsedTime = new Date(this.deadline - new Date().getTime());
            if(Date.parse(this.elapsedTime) >= 0) {
                this.requestAnimationId = requestAnimationFrame(this.tick);
            } else {
                this.reset();
            }
        },
        run() {
            this.endTime = '';
            this.deadline = new Date((this.minutes * 60) * 1000 + (this.seconds * 1000) + Date.now());
            this.isActive = true;
            this.requestAnimationId = requestAnimationFrame(this.tick);
        },
        fix() {
            cancelAnimationFrame(this.requestAnimationId)
            this.minutes = this.elapsedTime.getUTCMinutes();
            this.seconds = this.elapsedTime.getUTCSeconds();
            this.isActive = false;
        },
        reset() {
            const endTime = new Date();
            cancelAnimationFrame(this.requestAnimationId)
            this.minutes = 0;
            this.seconds = 0;
            this.deadline = null;
            this.isActive = false;
            this.elapsedTime = null;
            this.requestAnimationId = null;
            this.endTime = ` - ${endTime.getHours()}:${endTime.getMinutes()}:${endTime.getSeconds()}`;
        },
    },
};
</script>


<style>

.btnsvg {
    border: none;
    background: none;
}
.btn-left {
    position: absolute;
    top: 20px;
    left: 70px;
}
.btn-rigth {
    position: absolute;
    top: 20px;
    left: 135px;
}
.svg {
    fill: #9e9e9e;
}
.svg-active {
    fill: #eee;
}
.stopwatch {
    background-color: #696969;
    width: 225px;
    min-height: 180px;
    margin: 25px;
    color: #eee;
    box-shadow: 5px 5px 20px 11px #9e9e9e;
}
.stopwatch__status {
    position: absolute;
    width: 166px;
    height: 14px;
    left: 82px;
    top: 43px;
    font-size: 15px;
    color: #696969;
}
.stopwatch__add-counts input {
    height: 40px;
    width: 60px;
    margin-top: 10px;
    text-align: center;
    font-size: 20px;
    border: 2px solid #9e9e9e;
    border-radius: 5px;
    color: #06c;
}
.stopwatch__time {
    height: 60px;
    width: 100%;
    display: flex;
    align-items: center;
}
.stopwatch__time {
    border-bottom: 1px solid #9E9E9E;
    justify-content: center;
}
.stopwatch__time-active {
    border-bottom: 1px solid #eee;
}
.stopwatch__btns {
    position:relative;
    width: 225px;
    height: 60px;
}
.stopwatch__time > p {
    font-size: 22px;
    text-align: center;
    color: #9e9e9e;
}
.stopwatch__time-active > p {
    color: #eee;
}
.display {
    display: none;
}
</style>
