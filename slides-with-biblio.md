---
title-slide: false
bibliography: references.bib
csl: vancouver.csl
citeproc: true
theme: serif
background-color: "#ffffff"
transition: slide
navigationMode: linear
hash: true
---

:::: {.columns}
::: {.column width="50%"}

## Sample slides
#### PlaceHolderName
#### Universiti Malaysia Perlis
#### [placeholder@email.com](mailto:placeholder@email.com)

<audio id="bg-music" src="media/audio/sb.m4a" loop></audio>

<div id="audio-credit"
     style="position: absolute; bottom: 40px; right: 20px; font-size: 0.6em; opacity: 0.6;">
  Music: “Adrift” by Scott Buckley (CC BY 4.0)
</div>

<script>
  document.addEventListener('DOMContentLoaded', () => {
    const audio = document.getElementById('bg-music');
    const credit = document.getElementById('audio-credit');

    // hide credit by default
    credit.style.display = 'none';

    const test = new Audio('media/audio/bgm.mp3');

    test.addEventListener('canplaythrough', () => {
      // bgm.mp3 exists → use it, keep credit hidden
      audio.src = 'media/audio/bgm.mp3';
    }, { once: true });

    test.addEventListener('error', () => {
      // bgm.mp3 missing → sb.m4a will play → show credit
      credit.style.display = 'block';
    }, { once: true });

    document.addEventListener('click', () => {
      if (Reveal.getIndices().h === 0) {
        audio.volume = 0.5;
        audio.play();
      }
    }, { once: true });

    Reveal.on('slidechanged', (event) => {
      if (event.indexh > 0) { audio.pause(); }
      else { audio.play(); }
    });
  });
</script>

:::

::: {.column width="50%"}
![](media/pics/logo1.png)
:::

::::

---

:::: {.columns}
::: {.column width="50%"}
### Slide one
**Key Concepts:**
- Energy conservation per @carnot1824.
- $\Delta U = Q - W$
:::

::: {.column width="50%"}
![](media/pics/sample.png)
:::
::::

---

<span class="slide-title" data-title="My Hidden Slide Name"></span>

![](media/pics/wide.jpeg)

---

:::: {.columns}
::: {.column width="50%"}
### The Master Equation
The fundamental relation of thermodynamics:

$$\Delta U = Q - W$$

The work done $W$ is positive when the system expands against an external pressure.
:::

::: {.column width="50%"}
<video data-src="media/videos/sample.mp4" data-autoplay loop muted width="100%"></video>
:::

::::

---

:::: {.columns}
::: {.column width="50%"}
### Visualizing the Gas Law
**Interactive Model:**

- P, V, and T relationships.
- Use the slider to adjust pressure.
- Observe the phase boundary.
:::

::: {.column width="50%"}
<iframe 
  data-src="media/plots/sample.html" 
  width="100%" 
  height="500px" 
  style="border:none;" 
  scrolling="no">
</iframe>
:::
::::

----

:::: {.columns}
::: {.column width="50%"}
### Control Chart for Machine 1 (P=200kPa, T=338K)

<p>The control chart for Machine 1 shows the PartLength over time.</p>

:::

::: {.column width="50%"}
<iframe data-src='media/plots/control_chart_machine_1_P200_T338.html' width='100%' height='500px' style='border:none;'></iframe>
<!-- Replace with actual plot image if direct html widget is not possible for qcc -->
:::

::::

----

:::: {.columns}
::: {.column width="50%"}
### Process Capability Chart for Machine 1 (P=200kPa, T=338K)

<p>This chart visualizes the process capability of Machine 1 against the specified limits.</p>

:::

::: {.column width="50%"}
<iframe data-src='media/plots/process_capability_machine_1_P200_T338.html' width='100%' height='500px' style='border:none;'></iframe>
:::

::::

----

### Cpk for Machine 1 (P=200kPa, T=338K)

```{r}
# Filter data for Machine 1, Pressure = 200kPa, Temp = 338K
data_m1 <- subset(X011, Machine == 1 & Pressure == 200 & Temperature == 338)

LSL = 45
USL = 55
TARGET = 50

# Create a qcc object for capability analysis
qcc_obj_m1_cap <- qcc(data_m1$PartLength, type="xbar.one", plot=FALSE)

# Process Capability Analysis
pc_m1 <- process.capability(qcc_obj_m1_cap, spec.limits=c(LSL, USL), target=TARGET, plot=FALSE)

# Extract Cpk value
cpk_m1 <- round(pc_m1$cpk, 4)

cat("Cpk for Machine 1 (P=200kPa, T=338K): ", cpk_m1)
```

:::

::::

----

### Machine 1 Capability Evaluation

<p>To evaluate if Machine 1 is capable under these conditions, we consider the Cpk value. A Cpk value of 1.33 or higher generally indicates a capable process, while a Cpk between 1.0 and 1.33 suggests the process is adequate but may require close monitoring. A Cpk below 1.0 indicates the process is not capable.</p>

<p>Based on the calculated Cpk for Machine 1 (refer to Slide 3 for the specific value), we can determine its capability:</p>

<ul>
  <li>If Cpk is >= 1.33: Machine 1 is **capable**.</li>
  <li>If Cpk is between 1.0 and 1.33: Machine 1 is **adequate**.</li>
  <li>If Cpk is < 1.0: Machine 1 is **not capable**.</li>
</ul>

:::

::::

----

:::: {.columns}
::: {.column width="50%"}
### Control Chart for Machine 2 (P=200kPa, T=338K)

<p>The control chart for Machine 2 shows the PartLength over time.</p>

:::

::: {.column width="50%"}
<iframe data-src='media/plots/control_chart_machine_2_P200_T338.html' width='100%' height='500px' style='border:none;'></iframe>
:::

::::

----

:::: {.columns}
::: {.column width="50%"}
### Process Capability Chart for Machine 2 (P=200kPa, T=338K)

<p>This chart visualizes the process capability of Machine 2 against the specified limits.</p>

:::

::: {.column width="50%"}
<iframe data-src='media/plots/process_capability_machine_2_P200_T338.html' width='100%' height='500px' style='border:none;'></iframe>
:::

::::

----

### Cpk for Machine 2 (P=200kPa, T=338K)

```{r}
# Filter data for Machine 2, Pressure = 200kPa, Temp = 338K
data_m2 <- subset(X011, Machine == 2 & Pressure == 200 & Temperature == 338)

LSL = 45
USL = 55
TARGET = 50

# Create a qcc object for capability analysis
qcc_obj_m2_cap <- qcc(data_m2$PartLength, type="xbar.one", plot=FALSE)

# Process Capability Analysis
pc_m2 <- process.capability(qcc_obj_m2_cap, spec.limits=c(LSL, USL), target=TARGET, plot=FALSE)

# Extract Cpk value
cpk_m2 <- round(pc_m2$cpk, 4)

cat("Cpk for Machine 2 (P=200kPa, T=338K): ", cpk_m2)
```

:::

::::

----

### Machine 2 Capability Evaluation

<p>To evaluate if Machine 2 is capable under these conditions, we consider the Cpk value. A Cpk value of 1.33 or higher generally indicates a capable process, while a Cpk between 1.0 and 1.33 suggests the process is adequate but may require close monitoring. A Cpk below 1.0 indicates the process is not capable.</p>

<p>Based on the calculated Cpk for Machine 2 (refer to Slide 7 for the specific value), we can determine its capability:</p>

<ul>
  <li>If Cpk is >= 1.33: Machine 2 is **capable**.</li>
  <li>If Cpk is between 1.0 and 1.33: Machine 2 is **adequate**.</li>
  <li>If Cpk is < 1.0: Machine 2 is **not capable**.</li>
</ul>

:::

::::

----

:::: {.columns}
::: {.column width="50%"}
### Control Chart for Machine 3 (P=200kPa, T=338K)

<p>The control chart for Machine 3 shows the PartLength over time.</p>

:::

::: {.column width="50%"}
<iframe data-src='media/plots/control_chart_machine_3_P200_T338.html' width='100%' height='500px' style='border:none;'></iframe>
:::

::::

----

:::: {.columns}
::: {.column width="50%"}
### Process Capability Chart for Machine 3 (P=200kPa, T=338K)

<p>This chart visualizes the process capability of Machine 3 against the specified limits.</p>

:::

::: {.column width="50%"}
<iframe data-src='media/plots/process_capability_machine_3_P200_T338.html' width='100%' height='500px' style='border:none;'></iframe>
:::

::::

----

### Cpk for Machine 3 (P=200kPa, T=338K)

```{r}
# Filter data for Machine 3, Pressure = 200kPa, Temp = 338K
data_m3 <- subset(X011, Machine == 3 & Pressure == 200 & Temperature == 338)

LSL = 45
USL = 55
TARGET = 50

# Create a qcc object for capability analysis
qcc_obj_m3_cap <- qcc(data_m3$PartLength, type="xbar.one", plot=FALSE)

# Process Capability Analysis
pc_m3 <- process.capability(qcc_obj_m3_cap, spec.limits=c(LSL, USL), target=TARGET, plot=FALSE)

# Extract Cpk value
cpk_m3 <- round(pc_m3$cpk, 4)

cat("Cpk for Machine 3 (P=200kPa, T=338K): ", cpk_m3)
```

:::

::::

----

### Machine 3 Capability Evaluation

<p>To evaluate if Machine 3 is capable under these conditions, we consider the Cpk value. A Cpk value of 1.33 or higher generally indicates a capable process, while a Cpk between 1.0 and 1.33 suggests the process is adequate but may require close monitoring. A Cpk below 1.0 indicates the process is not capable.</p>

<p>Based on the calculated Cpk for Machine 3 (refer to Slide 11 for the specific value), we can determine its capability:</p>

<ul>
  <li>If Cpk is >= 1.33: Machine 3 is **capable**.</li>
  <li>If Cpk is between 1.0 and 1.33: Machine 3 is **adequate**.</li>
  <li>If Cpk is < 1.0: Machine 3 is **not capable**.</li>
</ul>

:::

::::

---
# Bibliography
<div id="refs"></div>
