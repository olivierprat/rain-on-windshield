# Rain on windshield

This project demonstrates an effect of rain drops falling on a glass surface and dripping down. It is based on **Alix Michel**'s original rain on window effect, slightly tweaked, so all credit goes to her. It works with HDRP and relies on a Custom Render Texture and shader graphs.

Press 'Play' to see the effect in action.

## Description

The scene has an instance of the **Quad_rainEffect** prefab which you can find, along every other asset necessary for the effect, in the Assets/RainOnWindow folder. This is basically a quad with the **RainOnGlass_Material**, a Lit shader using the **RainOnGlass** shader graph.

The **CRT_WindowRain** Custom Render Texture is updated through the **CRT_WindowRain_Material** based on the **CRT_WindowRain_Shader** shader graph.

### RainOnGlass shader
This shader uses the heightmap rendertexture to create a normal map effect and much of the shader graph could be simplified.

The main controls are:
* Rain:
    * *Normal Strength*: the intensity of the normal mapping
    * *RainFogTiling*: the tiling factor of the fog texture mask. The fog texture defines zones where the glass is blured to simulate a foggy effect on the glass. (see Smoothness)
* Smoothness:
    * *Smoothness Rain*: the material smoothness for the drops
    * *Global Smoothness 1 & 2*: controls the range of material smoothness as it is mapped to the Fog texture. For perctly clear glass, set this to 1 on both.

### CRT_WindowRain_Shader
This is where the dynamic rain effect happens.

The main controls are:

* *Droplets Intensity*: controls the height of each drop
* *Droplets Size*: the size of each drop
* *Droplets perFrame*: the number of drops created over the entire texture at each update
* *Droplets Fade Ratio*: how much previous drops are faded at each update. High values make the drops disappear very quickly. For water streaking effects, lower this to 0.0001
* *Gravity Force*: the amount of 'gravity', but reality velocity of the rains dropping down, for drops that fall down the window. Actually multiplied by the following value.
* *Gravity Standing Droplets*: same as above but for drops that tend to stick in place.
* *Laterial Force*: amount of speed pushing the drops to the edges. Used to simulate the window moving at speed in the Z direction
* *Wiper Min Max Radius*: the wiper rotation point is at the top (can be changed in the shader) and this defines in normalized coordinates the start and end distance of the wiper effect
* *Wiper Angle Range*: in radians the angle range of the wiper effect
* *Flow Map Weight*: the intensity of the flow map effect
* *Flow Map*: the flow map texture
* *Flow Map tiling*: how many times show the flow map be tiled
* *Clear*: clears the entire texture when enabled
