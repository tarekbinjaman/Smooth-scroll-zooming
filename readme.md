# Smooth scroll zooming

install framer-motion
~~~
npm install motion
~~~

## user guide
## 1. What is happening here?
You are making an image slowly zoom in (scale up) when you scroll down the page — but smoothly, like it’s floating, not jumping suddenly.

## 2. Imports:
You are importing tools from framer-motion:

motion → to animate HTML elements (like <motion.img>).

useScroll → to track how much you have scrolled.

useTransform → to change scroll values into scale values.

useSpring → to make the animation feel smooth and springy.

## 3. Key parts:

~~~
const { scrollYProgress } = useScroll();
~~~

Tracks how far you have scrolled.

scrollYProgress value is between 0 (top) and 1 (bottom).

~~~
const rawScale = useTransform(scrollYProgress, [0, 1], [1, 1.6]);
~~~

Converts the scroll into a scale value:

When scroll is 0 → image scale is 1 (normal size).

When scroll is 1 → image scale is 1.6 (bigger).

~~~
const scale = useSpring(rawScale, {
    stiffness: 60,
    damping: 40,
    mass: 1
});
~~~

Makes the zooming smooth like a spring:

stiffness: how hard the spring is (lower = slower movement).

damping: how quickly it stops (higher = softer stop).

mass: how heavy it feels.

## 4. The HTML Part:

~~~
                    <div
                className='flex justify-center items-center border border-amber-300'
                style={{
                    height: '400px',
                    width: '800px',
                    margin: '0 auto',
                    overflow: 'hidden',
                    position: 'relative'
                }}
            >
                <motion.img
                    src="https://t4.ftcdn.net/jpg/06/81/35/49/360_F_681354997_LjEvGcOg8YeK58dsOfGn8wJV5IFvxI77.jpg"
                    alt="Moving Image"
                    style={{
                        width: '100%',
                        height: '100%',
                        objectFit: 'cover',
                        scale: scale,
                    }}
                />
            </div>
~~~

A box (800px wide, 400px tall) to hold the image.

The box is centered and has a yellow border.

Inside it:

The image that gets animated!

It scales bigger when you scroll, because of the scale: scale style.






## Full code:
~~~
const Home = () => {
    const { scrollYProgress } = useScroll();
    const rawScale = useTransform(scrollYProgress, [0, 1], [1, 1.6]);

    const scale = useSpring(rawScale, {
        stiffness: 60,   // how stiff the spring is (lower = softer)
        damping: 40,     // how much resistance (higher = more smooth stop)
        mass: 1          // how heavy the object feels
    });

    return (
        <div>
                    <div
                className='flex justify-center items-center border border-amber-300'
                style={{
                    height: '400px',
                    width: '800px',
                    margin: '0 auto',
                    overflow: 'hidden',
                    position: 'relative'
                }}
            >
                <motion.img
                    src="https://t4.ftcdn.net/jpg/06/81/35/49/360_F_681354997_LjEvGcOg8YeK58dsOfGn8wJV5IFvxI77.jpg"
                    alt="Moving Image"
                    style={{
                        width: '100%',
                        height: '100%',
                        objectFit: 'cover',
                        scale: scale,
                    }}
                />
            </div>
                </div>
    );
};

export default Home;
~~~