<script lang="ts">
  import { slide } from "svelte/transition";
  import SidebarSection from "./SidebarSection.svelte";
  import InputLabel from "./InputLabel.svelte";
  import AlignmentPicker from "./AlignmentPicker.svelte";
  import {
    screenLayoutState,
    webcamLayoutState,
    WebcamShape,
    webcamShapeOptions,
  } from "../stores.js";
  import { titleCase } from "../utils/titleCase.js";
  import Select from "./Select.svelte";
  import RangeInput from "./RangeInput.svelte";
</script>

<SidebarSection title="Layout">
  <div class="grid grid-cols-2 gap-x-4 gap-y-6">
    <div>
      <InputLabel>Webcam Position</InputLabel>
      <div class="mb-1" />
      <AlignmentPicker
        bind:horizAlign={$webcamLayoutState.horizAlign}
        bind:vertAlign={$webcamLayoutState.vertAlign}
      />
    </div>
    <div>
      <!-- <InputLabel>Screen Position</InputLabel>
      <div class="mb-1" />
      <AlignmentPicker
        bind:horizAlign={$screenLayoutState.horizAlign}
        bind:vertAlign={$screenLayoutState.vertAlign}
      /> -->
    </div>
    <!-- Webcam shape/width -->
    <!-- <div class="col-span-2">
      <Select
        title="Webcam shape"
        name="webcamShape"
        options={webcamShapeOptions.map((val) => ({
          title: titleCase(val),
          value: val,
        }))}
        bind:value={$webcamLayoutState.shape}
        isDropdown={false}
      />
    </div> -->
    <RangeInput
      name="webcamWidth"
      title="Webcam Width"
      bind:value={$webcamLayoutState.size}
      min={0}
      max={1}
      step={0.02}
    />
    {#if $webcamLayoutState.shape === WebcamShape.initial}
      <RangeInput
        name="webcamBorderRadius"
        title="Border radius"
        bind:value={$webcamLayoutState.borderRadius}
        min={0}
        max={1}
        step={0.02}
      />
    {/if}
  </div>
</SidebarSection>
