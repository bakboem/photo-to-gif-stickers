---
name: Cartoon caricature GIF stickers from a photo
description: >-
  Use this when the user wants exaggerated cartoon stickers or GIFs of
  themselves (or a person who agreed) from a reference photo, in one consistent
  style.
---
# Recipe (verified, produced a 2-frame sticker GIF the user approved)

1. Reference photo: use the user's attached photo path in `reference_image_paths` for every first frame. Identify 3-4 identity anchors (e.g. cap color, glasses shape, beard) and repeat them in every prompt so the character stays recognizable.
2. Style line to repeat in every prompt: "Exaggerated cartoon caricature, thick bold outlines, flat bright colors, big head small body, sticker style, solid light-gray background, white sticker border", aspect_ratio 1:1.
3. Frame A: one GenerateImage per scene with the photo as reference. Put outfit/props/joke in the prompt (tech humor works well: hacker hoodie with five monitors, robot armor + VR headset, Hawaiian shirt + giant DEPLOY button, astronaut on a flying laptop rocket). Say "Frame A of an animation" and describe the starting pose.
4. Frame B: a second GenerateImage using the generated frame A as the only reference. Prompt: "Frame B of the same sticker animation, identical character, outfit, framing, colors and style as the reference. Change only the pose and expression: ..." Describe the opposite/escalated emotion (calm -> panic, relaxed -> flexing).
5. Assemble with Python Pillow: resize to 512x512, build frames: A held with a tiny 3px bob (4 frames, 150ms), A hold 500ms, then ~14 frames of B with random +-9px offset (ImageChops.offset) at 70ms, every other frame blended 18% red, final B hold 400ms. Convert each frame to adaptive palette (128 colors), save with save_all, loop=0, optimize=True, disposal=2. Result is about 2 MB.
6. Deliver the GIF first; show one finished sample and ask before making the rest.
7. Rules learned: don't add brand or name text unless asked; keep the signature look recognizable in every frame; generate image calls can be slow, run them in parallel but expect interruptions if the user sends new messages.
