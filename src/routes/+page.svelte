<script lang="ts">
    import gsap, { Linear } from 'gsap'
    import { onMount } from 'svelte'

    const randMinMax = (t: number, n: number, a?: number) => {
        let r = t+Math.random()*(n-t);
        return a && (r=Math.round(r)),r
    };

    onMount(() => {
        let w = document.body.clientWidth,
            h = document.body.clientHeight,
            numberOfStars = 100,
            PosX = 0,
            PosY = 0;

        let tl = gsap.timeline();

        console.log('hello world');

        const arr = [];
        arr.length = 100;

        for (let i = 0; i < numberOfStars; i++) {
            const starEle = document.createElement('sapn');
            starEle.classList.add('star');

            console.log('i:', i);
            console.log('hello world');

            PosX = Math.floor(Math.random() * w);
            PosY = 0;
            const size = Math.floor(Math.random()* 30);

            document.body.appendChild(starEle)

            if (i%2 == 0){
                gsap.set(starEle, {backgroundColor: "#ffcd5e"});
            }
            if (i%3 == 0){
                gsap.set(starEle, {backgroundColor: "#fe8261"});
            }

            gsap.set(starEle, {
                x: PosX,
                y: PosY - (size * 5),
                width: size,
                height: size,
            });

            tl.to(
                starEle,
                randMinMax(5, 7),
                {
                    x:PosX,
                    y: h + (size *2),
                    opacity:1,
                    repeat:-1,
                    repeatDelay: randMinMax(0, 1),
                    ease: Linear.easeNone
                },
                randMinMax(0, 4),
            );

            console.log(i);
        }
    });

</script>

<svelte:head>
	<title>💗Draw a heart💗</title>
</svelte:head>

<svg class="heart-loader" viewBox="0 0 90 90" version="1.1">
    <g class="heart-loader__group">
        <path class="heart-loader__square" stroke-width="1" fill="none" d="M0,30 0,90 60,90 60,30z" />
        <path class="heart-loader__circle m--left" stroke-width="1" fill="none" d="M60,60 a30,30 0 0,1 -60,0 a30,30 0 0,1 60,0" />
        <path class="heart-loader__circle m--right" stroke-width="1" fill="none" d="M60,60 a30,30 0 0,1 -60,0 a30,30 0 0,1 60,0" />
        <path class="heart-loader__heartPath" stroke-width="2" d="M60,30 a30,30 0 0,1 0,60 L0,90 0,30 a30,30 0 0,1 60,0" />
    </g>
</svg>

<style lang="scss">
@use "sass:math";

$strokeColor: rgb(77, 161, 185);
$heartColor: #db3434;
$size: 300px; // change this to manipulate overall size
$totalAnim: 7s;
$delay: 0.1s;
$squareLen: 240;
$circleLen: 188.522;
$heartLen: 308.522;
$svgSize: 90px;
$circleW: 60px;

$white: #fff;
$red:   #f53;
$green: #3c4d27;

// angle of loop
$radius-small:   2em;
$radius-big:     10em;

.heart-loader {
    position: absolute;
    display: block;
    left: 50%;
    top: 50%;
    margin-top: math.div($size, -2);
    width: $size;
    height: $size;
    overflow: visible;


    &__group {
        transform-origin: 0 $svgSize;
        animation: group-anim $totalAnim $delay infinite;
    }

    &__square {
        stroke: $strokeColor;
        stroke-dasharray: $squareLen, $squareLen;
        stroke-dashoffset: $squareLen;
        animation: square-anim $totalAnim $delay infinite;
    }

    &__circle {
        stroke: $strokeColor;
        stroke-dasharray: $circleLen, $circleLen;
        stroke-dashoffset: $circleLen;
        transform-origin: $circleW math.div($circleW, 2);

        &.m--left {
            animation: left-circle-anim $totalAnim $delay infinite;
        }

        &.m--right {
            animation: right-circle-anim $totalAnim $delay infinite;
        }
    }

    &__heartPath {
        stroke: $heartColor;
        fill: transparent;
        stroke-dasharray: $heartLen, $heartLen;
        stroke-dashoffset: $heartLen;
        animation: heart-anim $totalAnim $delay infinite;
    }
}
@keyframes square-anim {
    12% {
        stroke-dashoffset: 0;
    }
    43% {
        stroke-dashoffset: 0;
        opacity: 1;
    }
    85% {
        stroke-dashoffset: 0;
        opacity: 0;
    }
    100% {
        stroke-dashoffset: 0;
        opacity: 0;
    }
}
@keyframes left-circle-anim {
    12% {
        stroke-dashoffset: $circleLen;
    }
    31% {
        stroke-dashoffset: 0;
        transform: translateY(0);
    }
    41% {
        stroke-dashoffset: 0;
        transform: translateY(math.div($circleW, -2));
    }
    43% {
        stroke-dashoffset: 0;
        transform: translateY(math.div($circleW, -2));
        opacity: 1;
    }
    85% {
        stroke-dashoffset: 0;
        transform: translateY(math.div($circleW, -2));
        opacity: 0;
    }
    100% {
        stroke-dashoffset: 0;
        transform: translateY(math.div($circleW, -2));
        opacity: 0;
    }
}
@keyframes right-circle-anim {
    12% {
        stroke-dashoffset: $circleLen;
    }
    31% {
        stroke-dashoffset: 0;
        transform: translateX(0);
    }
    41% {
        stroke-dashoffset: 0;
        transform: translateX(math.div($circleW, 2));
    }
    43% {
        stroke-dashoffset: 0;
        transform: translateX(math.div($circleW, 2));
        opacity: 1;
    }
    85% {
        stroke-dashoffset: 0;
        transform: translateX(math.div($circleW, 2));
        opacity: 0;
    }
    100% {
        stroke-dashoffset: 0;
        transform: translateX(math.div($circleW, 2));
        opacity: 0;
    }
}
@keyframes group-anim {
    43% {
        transform: rotate(0);
    }
    54% {
        transform: rotate(-45deg);
    }
    90% {
        transform: rotate(-45deg);
        opacity: 1;
    }
    97% {
        transform: rotate(-45deg);
        opacity: 0;
    }
    100% {
        transform: rotate(-45deg);
        opacity: 0;
    }
}
@keyframes heart-anim {
    55% {
        stroke-dashoffset: $heartLen;
        fill: transparent;
    }
    70% {
        stroke-dashoffset: 0;
        fill: transparent;
    }
    87% {
        stroke-dashoffset: 0;
        fill: $heartColor;
    }
    100% {
        stroke-dashoffset: 0;
        fill: $heartColor;
    }
}
</style>
