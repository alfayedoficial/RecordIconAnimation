# 🚀 How to Create a Pulse Effect of Record Video in Jetpack Compose

Welcome, developers! 👋

This project demonstrates how to create an engaging **Pulse Effect** animation in Jetpack Compose, perfect for highlighting a **record video icon** and capturing user attention 🎯.

---

## 📹 Demo Video

Check out the Pulse Effect in action by watching the demo video below:

[![Watch the Demo]](https://github.com/user-attachments/assets/07ded946-33dd-4bb1-a031-1aece28bf84b)

---

## 🚀 Overview

The Pulse Effect creates a visual animation where a record icon pulses to attract attention. This effect is created by combining two pulsating animations, giving a dynamic and layered look.

### 🛠️ Features

- **Double Pulse Effect**: Two consecutive pulses to enhance visual engagement.
- **Customizable Parameters**: Easily adjust scale, duration, color, and shape.
- **Jetpack Compose**: Uses modern Jetpack Compose features for UI development.

---

## 📦 Project Structure
- **MainScreen.kt** - Composable function displaying the record icon with the pulse effect.
- **PulseEffectModifier.kt** - Custom Modifier for the pulse and double pulse effect.
- **README.md** - Project documentation.
  
---

## 🧩 How to Use the Pulse Effect Modifier

### 1. Define the Pulse Effect Modifier

The `pulseEffect` modifier creates a pulsating background effect.

```kotlin
@Composable
fun Modifier.pulseEffect(
    targetScale: Float = 1.5f,
    initialScale: Float = 1f,
    brush: Brush = SolidColor(Color.Red.copy(alpha = 0.32f)),
    shape: Shape = CircleShape,
    animationSpec: DurationBasedAnimationSpec<Float> = tween(1200)
): Modifier {
    val pulseTransition = rememberInfiniteTransition()
    val pulseScale by pulseTransition.animateFloat(
        initialValue = initialScale,
        targetValue = targetScale,
        animationSpec = infiniteRepeatable(animationSpec),
    )
    val pulseAlpha by pulseTransition.animateFloat(
        initialValue = 1f,
        targetValue = 0f,
        animationSpec = infiniteRepeatable(animationSpec),
    )

    return this.drawBehind {
        val outline = shape.createOutline(size, layoutDirection, this)
        scale(pulseScale) {
            drawOutline(outline, brush, pulseAlpha)
        }
    }
}

```
### 2. Add the Double Pulse Effect

The `doublePulseEffect` modifier applies two consecutive pulse effects.

```kotlin
@Composable
fun Modifier.doublePulseEffect(
    targetScale: Float = 1.5f,
    initialScale: Float = 1f,
    brush: Brush = SolidColor(Color.Red.copy(alpha = 0.32f)),
    shape: Shape = CircleShape,
    duration: Int = 1200
): Modifier {
    return this
        .pulseEffect(targetScale, initialScale, brush, shape, tween(duration, easing = FastOutSlowInEasing))
        .pulseEffect(targetScale, initialScale, brush, shape, tween((duration * 0.7).toInt(), delayMillis = (duration * 0.3).toInt(), easing = LinearEasing))
}
```
### 3. Apply the Pulse Effect in `MainScreen`

```kotlin
@Composable
fun MainScreen(modifier: Modifier = Modifier) {
    var startRecording by remember { mutableStateOf(false) }

    Box(
        modifier = modifier.fillMaxSize(),
        contentAlignment = Alignment.Center
    ) {
        IconButton(
            modifier = Modifier
                .size(42.dp)
                .then(if (startRecording) Modifier.doublePulseEffect() else Modifier),
            onClick = { startRecording = !startRecording }
        ) {
            Icon(
                painter = painterResource(id = R.drawable.ic_map_recored),
                modifier = Modifier.fillMaxSize(),
                contentDescription = "Record Video",
                tint = Color.Red
            )
        }

        Text(
            text = if (startRecording) "Recording" else "Record",
            color = Color.Black,
            fontSize = 13.sp,
            fontWeight = FontWeight.Bold,
            textAlign = TextAlign.Center,
            modifier = Modifier.align(Alignment.Center).padding(top = if (startRecording) 75.dp else 55.dp)
        )
    }
}

```
## 🛠️ Customization Options

You can customize the pulse effect by adjusting the following parameters:

- **`targetScale`**: The maximum scale the pulse grows to.
- **`initialScale`**: The starting scale of the pulse.
- **`brush`**: The color or gradient of the pulse.
- **`shape`**: The shape of the pulse (default is `CircleShape`).
- **`duration`**: Duration of the pulse animation in milliseconds.

---

## 🔗 References

- **GitHub Repo**: [Pulse Effect in Jetpack Compose](https://lnkd.in/gpsHhVnd)  
- **Medium Article**: [How to Create a Pulse Effect in Jetpack Compose](https://lnkd.in/dCRvqhax)


