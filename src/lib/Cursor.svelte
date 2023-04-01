<script lang="ts">
  import { onMount } from "svelte";
  import { spring } from "svelte/motion";
  import checkMobile from "../utils/check_mobile";
  import { getScreenSize } from "../utils/screen_size";
  export let cursorColor = "royalblue"; // #ff3e00

  $: isMobile = checkMobile();
  $: isLocked = false;
  $: isFullScreen = false;
  $: srcSize = getScreenSize();
  $: intractableElements = document.querySelectorAll("a, button");
  $: pointerEvent = undefined;

  const mousePos = { x: -16, y: -16 };
  const defaultSizeInside = { width: 24, height: 24 };
  const defaultSizeOutside = { width: 48, height: 48 };
  const defaultMouseDownSizeInside = { width: 48, height: 48 };
  const defaultMouseDownSizeOutside = { width: 64, height: 64 };

  const coordsInside = spring(mousePos, {
    stiffness: 0.5,
    damping: 1,
  });

  const coordsOutside = spring(mousePos, {
    stiffness: 0.3,
    damping: 1,
  });

  const coordsInsideInvert = spring(mousePos, {
    stiffness: 0.5,
    damping: 1,
  });

  const coordsOutsideInvert = spring(mousePos, {
    stiffness: 0.3,
    damping: 1,
  });

  const sizeInside = spring(defaultSizeInside, {
    stiffness: 0.45,
    damping: 1,
  });

  const sizeOutside = spring(defaultSizeOutside, {
    stiffness: 0.25,
    damping: 1,
  });

  const sizeInsideInvert = spring(defaultSizeInside, {
    stiffness: 0.45,
    damping: 1,
  });

  const sizeOutsideInvert = spring(defaultSizeOutside, {
    stiffness: 0.25,
    damping: 1,
  });

  const borderRadiusInside = spring(48, {
    stiffness: 0.3,
    damping: 1,
  });

  const borderRadiusOutside = spring(48, {
    stiffness: 0.3,
    damping: 1,
  });
  const borderRadiusInsideInvert = spring(48, {
    stiffness: 0.3,
    damping: 1,
  });

  const borderRadiusOutsideInvert = spring(48, {
    stiffness: 0.3,
    damping: 1,
  });

  const fillOpacityInside = spring(0, {
    stiffness: 0.1,
    damping: 0.25,
  });

  const fillOpacityOutside = spring(0, {
    stiffness: 0.1,
    damping: 0.25,
  });

  const fillOpacityInsideInvert = spring(1, {
    stiffness: 0.1,
    damping: 0.25,
  });

  const fillOpacityOutsideInvert = spring(0.5, {
    stiffness: 0.1,
    damping: 0.25,
  });

  const strokeOpacityInside = spring(1, {
    stiffness: 0.1,
    damping: 0.25,
  });

  const strokeOpacityOutside = spring(0.5, {
    stiffness: 0.1,
    damping: 0.25,
  });

  const strokeOpacityInsideInvert = spring(1, {
    stiffness: 0.1,
    damping: 0.25,
  });

  const strokeOpacityOutsideInvert = spring(0.5, {
    stiffness: 0.1,
    damping: 0.25,
  });

  window.onresize = () => {
    srcSize = getScreenSize();
    if (isFullScreen) {
      let mousePos = { x: srcSize.width / 2, y: srcSize.height / 2 };
      coordsInside.set(mousePos);
      coordsOutside.set(mousePos);
      sizeInside.set({ width: srcSize.width, height: srcSize.height });
      sizeOutside.set(
        { width: srcSize.width, height: srcSize.height },
        { hard: true }
      );
    }
  };

  document.onpointerdown = (event) => {
    pointerEvent = event;
    if (event.pointerType === "touch") {
      let mousePos = {
        x: event.x,
        y: event.y,
      };
      if (!isLocked) {
        fillOpacityInsideInvert.set(1);
        fillOpacityOutsideInvert.set(0.25);
        strokeOpacityInsideInvert.set(1);
        strokeOpacityOutsideInvert.set(0.25);
        coordsInsideInvert.set(mousePos, { hard: true });
        coordsOutsideInvert.set(mousePos, { hard: true });
        if (!isFullScreen) {
          fillOpacityInside.set(1);
          fillOpacityOutside.set(0.25);
          strokeOpacityInside.set(1);
          strokeOpacityOutside.set(0.25);
          coordsInside.set(mousePos, { hard: true });
          coordsOutside.set(mousePos, { hard: true });
        }
      }
    }

    if (!isLocked) {
      sizeInsideInvert.set(defaultMouseDownSizeInside);
      sizeOutsideInvert.set(defaultMouseDownSizeOutside);
      if (!isFullScreen) {
        sizeInside.set(defaultMouseDownSizeInside);
        sizeOutside.set(defaultMouseDownSizeOutside);
      }
    }
  };

  document.onpointermove = (event) => {
    pointerEvent = event;
    let mousePos = { x: event.x, y: event.y };
    if (!isLocked) {
      coordsInsideInvert.set(mousePos);
      coordsOutsideInvert.set(mousePos);
      if (!isFullScreen) {
        coordsInside.set(mousePos);
        coordsOutside.set(mousePos);
        fillOpacityInside.set(1);
        fillOpacityOutside.set(0.5);
      }
    }
  };

  document.onpointerup = (event) => {
    pointerEvent = event;
    if (event.pointerType === "touch") {
      if (!isLocked) {
        fillOpacityInsideInvert.set(0);
        fillOpacityOutsideInvert.set(0);
        strokeOpacityInsideInvert.set(0);
        strokeOpacityOutsideInvert.set(0);
        if (!isFullScreen) {
          fillOpacityInside.set(0);
          fillOpacityOutside.set(0);
          strokeOpacityInside.set(0);
          strokeOpacityOutside.set(0);
        }
      }
    }
    if (!isLocked) {
      sizeInsideInvert.set(defaultSizeInside);
      sizeOutsideInvert.set(defaultSizeOutside);
      if (!isFullScreen) {
        sizeInside.set(defaultSizeInside);
        sizeOutside.set(defaultSizeOutside);
      }
    }
  };

  document.ontouchmove = (event) => {
    pointerEvent = event;
    let mousePos = { x: event.touches[0].clientX, y: event.touches[0].clientY };
    if (!isLocked) {
      coordsInsideInvert.set(mousePos);
      coordsOutsideInvert.set(mousePos);
      if (!isFullScreen) {
        coordsInside.set(mousePos);
        coordsOutside.set(mousePos);
      }
    }
  };

  document.ontouchend = (event) => {
    pointerEvent = event;
    if (!isLocked) {
      fillOpacityInsideInvert.set(0);
      fillOpacityOutsideInvert.set(0);
      sizeInsideInvert.set(defaultSizeInside);
      sizeOutsideInvert.set(defaultSizeOutside);
      strokeOpacityInsideInvert.set(0);
      strokeOpacityOutsideInvert.set(0);
      if (!isFullScreen) {
        fillOpacityInside.set(0);
        fillOpacityOutside.set(0);
        sizeInside.set(defaultSizeInside);
        sizeOutside.set(defaultSizeOutside);
        strokeOpacityInside.set(0);
        strokeOpacityOutside.set(0);
      }
    }
  };

  function handleMouseOver(item: Element) {
    isLocked = true;
    const rect = item.getBoundingClientRect();
    let mousePos = {
      x: rect.x + rect.width / 2,
      y: rect.y + rect.height / 2,
    };
    const rectSize = { width: rect.width + 8, height: rect.height + 8 };
    if (!isFullScreen) {
      fillOpacityInside.set(0);
      fillOpacityOutside.set(0);
      strokeOpacityInside.set(1);
      strokeOpacityOutside.set(0);
      borderRadiusInside.set(12);
      borderRadiusOutside.set(12);
      coordsInside.set(mousePos);
      coordsOutside.set(mousePos);
      sizeInside.set(rectSize);
      sizeOutside.set(rectSize);
    }
    fillOpacityInsideInvert.set(0);
    fillOpacityOutsideInvert.set(0);
    strokeOpacityInsideInvert.set(1);
    strokeOpacityOutsideInvert.set(0);
    borderRadiusInsideInvert.set(12);
    borderRadiusOutsideInvert.set(12);
    coordsInsideInvert.set(mousePos);
    coordsOutsideInvert.set(mousePos);
    sizeInsideInvert.set(rectSize);
    sizeOutsideInvert.set(rectSize);
  }

  function handleMouseDown(item: Element) {
    const rect = item.getBoundingClientRect();
    const rectSizeInside = { width: rect.width, height: rect.height };
    const rectSizeOutside = {
      width: rect.width + 16,
      height: rect.height + 16,
    };
    if (!isFullScreen) {
      fillOpacityOutside.set(0.25);
      strokeOpacityInside.set(0);
      strokeOpacityOutside.set(0.25);
      borderRadiusInside.set(8);
      borderRadiusOutside.set(16);
      sizeInside.set(rectSizeInside);
      sizeOutside.set(rectSizeOutside);
    }
    fillOpacityOutsideInvert.set(0.25);
    strokeOpacityInsideInvert.set(0);
    strokeOpacityOutsideInvert.set(0.25);
    borderRadiusInsideInvert.set(8);
    borderRadiusOutsideInvert.set(16);
    sizeInsideInvert.set(rectSizeInside);
    sizeOutsideInvert.set(rectSizeOutside);
  }

  function handleMouseUp(item: Element) {
    const rect = item.getBoundingClientRect();
    const rectSize = { width: rect.width + 8, height: rect.height + 8 };
    if (!isFullScreen) {
      fillOpacityOutside.set(0);
      strokeOpacityInside.set(1);
      strokeOpacityOutside.set(0);
      borderRadiusInside.set(12);
      borderRadiusOutside.set(12);
      sizeInside.set(rectSize);
      sizeOutside.set(rectSize);
    }
    fillOpacityOutsideInvert.set(0);
    strokeOpacityInsideInvert.set(1);
    strokeOpacityOutsideInvert.set(0);
    borderRadiusInsideInvert.set(12);
    borderRadiusOutsideInvert.set(12);
    sizeInsideInvert.set(rectSize);
    sizeOutsideInvert.set(rectSize);
  }

  function handleMouseLeave() {
    isLocked = false;
    if (!isFullScreen) {
      fillOpacityInside.set(1);
      fillOpacityOutside.set(0.5);
      strokeOpacityInside.set(1);
      strokeOpacityOutside.set(0.25);
      borderRadiusInside.set(48);
      borderRadiusOutside.set(48);
      sizeInside.set(defaultSizeInside);
      sizeOutside.set(defaultSizeOutside);
    }
    fillOpacityInsideInvert.set(1);
    fillOpacityOutsideInvert.set(0.25);
    strokeOpacityInsideInvert.set(1);
    strokeOpacityOutsideInvert.set(0.25);
    borderRadiusInsideInvert.set(48);
    borderRadiusOutsideInvert.set(48);
    sizeInsideInvert.set(defaultSizeInside);
    sizeOutsideInvert.set(defaultSizeOutside);
  }

  function resetCursor() {
    isLocked = false;
    // isFullScreen = false;
    if (pointerEvent !== undefined) {
      if (pointerEvent.type !== "touchend") {
        let mousePos = { x: pointerEvent.x, y: pointerEvent.y };
        coordsInside.set(mousePos, { hard: true });
        coordsOutside.set(mousePos, { hard: true });
      }

      if (
        pointerEvent.pointerType === "touch" ||
        pointerEvent.type === "touchend"
      ) {
        fillOpacityInside.set(0);
        fillOpacityOutside.set(0);
        fillOpacityInsideInvert.set(0);
        fillOpacityOutsideInvert.set(0);
        strokeOpacityInside.set(0);
        strokeOpacityOutside.set(0);
        strokeOpacityInsideInvert.set(0);
        strokeOpacityOutsideInvert.set(0);
      } else {
        fillOpacityInside.set(1);
        fillOpacityOutside.set(0.5);
        fillOpacityInsideInvert.set(1);
        fillOpacityOutsideInvert.set(0.25);
        strokeOpacityInside.set(1);
        strokeOpacityOutside.set(0.25);
        strokeOpacityInsideInvert.set(1);
        strokeOpacityOutsideInvert.set(0.25);
      }
    } else {
      fillOpacityInside.set(1);
      fillOpacityOutside.set(0.5);
      fillOpacityInsideInvert.set(1);
      fillOpacityOutsideInvert.set(0.25);
      strokeOpacityInside.set(1);
      strokeOpacityOutside.set(0.25);
      strokeOpacityInsideInvert.set(1);
      strokeOpacityOutsideInvert.set(0.25);
    }
    borderRadiusInside.set(48);
    borderRadiusOutside.set(48);
    borderRadiusInsideInvert.set(48);
    borderRadiusOutsideInvert.set(48);
    sizeInside.set(defaultSizeInside);
    sizeOutside.set(defaultSizeOutside);
    sizeInsideInvert.set(defaultSizeInside);
    sizeOutsideInvert.set(defaultSizeOutside);
  }

  export function updateIntractableElements() {
    intractableElements.forEach((item) => {
      item.removeEventListener("mouseover", () => {
        handleMouseOver(item);
      });
      item.removeEventListener("mousedown", () => {
        handleMouseDown(item);
      });
      item.removeEventListener("mouseup", () => {
        handleMouseUp(item);
      });
      item.removeEventListener("mouseleave", () => {
        handleMouseLeave();
      });
    });
    resetCursor();
    intractableElements = document.querySelectorAll("a, button");
    intractableElements.forEach((item) => {
      item.addEventListener("mouseover", () => {
        handleMouseOver(item);
      });
      item.addEventListener("mousedown", () => {
        handleMouseDown(item);
      });
      item.addEventListener("mouseup", () => {
        handleMouseUp(item);
      });
      item.addEventListener("mouseleave", () => {
        handleMouseLeave();
      });
    });
  }

  export function enterFullScreen(event?: PointerEvent) {
    isLocked = true;
    isFullScreen = true;

    if (event === undefined) {
      event = pointerEvent;
    }

    if (event !== undefined) {
      let mousePos = { x: event.x, y: event.y };
      coordsInsideInvert.set(mousePos);
      coordsOutsideInvert.set(mousePos);
    }

    if (event !== undefined && event.pointerType === "touch") {
      isLocked = false;
      fillOpacityInside.set(0);
      fillOpacityOutside.set(0);
      fillOpacityInsideInvert.set(0);
      fillOpacityOutsideInvert.set(0);
      strokeOpacityInside.set(0);
      strokeOpacityOutside.set(0);
      strokeOpacityInsideInvert.set(0);
      strokeOpacityOutsideInvert.set(0);
    } else {
      fillOpacityInsideInvert.set(1);
      fillOpacityOutsideInvert.set(0.5);
      strokeOpacityInside.set(1);
      strokeOpacityOutside.set(0.25);
      strokeOpacityInsideInvert.set(1);
      strokeOpacityOutsideInvert.set(0.25);
    }

    let mousePos = { x: srcSize.width / 2, y: srcSize.height / 2 };
    coordsInside.set(mousePos);
    coordsOutside.set(mousePos);

    sizeInside.set(
      { width: srcSize.width, height: srcSize.height },
      { soft: true }
    );
    sizeOutside.set(
      { width: srcSize.width, height: srcSize.height },
      { hard: true }
    );
    fillOpacityInside.set(1);
    fillOpacityOutside.set(0.5);
    borderRadiusInside.set(0, { soft: true });
    borderRadiusOutside.set(0);
    sizeInsideInvert.set(defaultSizeInside);
    sizeOutsideInvert.set(defaultSizeOutside);
    borderRadiusInsideInvert.set(48);
    borderRadiusOutsideInvert.set(48);
  }

  export function exitFullScreen(event?: PointerEvent) {
    isLocked = false;
    isFullScreen = false;

    if (event === undefined) {
      event = pointerEvent;
    }

    if (event !== undefined) {
      let mousePos = { x: event.x, y: event.y };
      coordsInside.set(mousePos, { hard: true });
      coordsOutside.set(mousePos, { hard: true });
    }

    if (event !== undefined && event.pointerType === "touch") {
      fillOpacityInside.set(0);
      fillOpacityOutside.set(0);
      fillOpacityInsideInvert.set(0);
      fillOpacityOutsideInvert.set(0);
      strokeOpacityInside.set(0);
      strokeOpacityOutside.set(0);
      strokeOpacityInsideInvert.set(0);
      strokeOpacityOutsideInvert.set(0);
    }
    borderRadiusInside.set(48);
    borderRadiusOutside.set(48);
    sizeInside.set(defaultSizeInside);
    sizeOutside.set(defaultSizeOutside);
  }

  onMount(() => {
    updateIntractableElements();
  });
</script>

{#if !isMobile}
  <div class:disable-pointer={isFullScreen}>
    <svg>
      <rect
        class="outside"
        fill={cursorColor}
        fill-opacity={$fillOpacityOutside}
        stroke={"#ffffff"}
        stroke-width={"2px"}
        stroke-opacity={$strokeOpacityOutside}
        x={$coordsOutside.x - $sizeOutside.width / 2}
        y={$coordsOutside.y - $sizeOutside.height / 2}
        rx={$borderRadiusOutside}
        ry={$borderRadiusOutside}
        width={$sizeOutside.width}
        height={$sizeOutside.height}
      />
      <rect
        class="Inside"
        fill={cursorColor}
        fill-opacity={$fillOpacityInside}
        stroke={isLocked ? cursorColor : "transparent"}
        stroke-width={isLocked ? "2px" : "0"}
        stroke-opacity={$strokeOpacityInside}
        x={$coordsInside.x - $sizeInside.width / 2}
        y={$coordsInside.y - $sizeInside.height / 2}
        rx={$borderRadiusInside}
        ry={$borderRadiusInside}
        width={$sizeInside.width}
        height={$sizeInside.height}
      />
    </svg>
  </div>
  <div class="invert">
    <svg>
      <rect
        class="outside"
        fill={"#ffffff"}
        fill-opacity={isFullScreen ? $fillOpacityOutsideInvert : 0}
        stroke={isFullScreen ? "#ffffff" : "transparent"}
        stroke-width={"2px"}
        stroke-opacity={isFullScreen && $strokeOpacityOutsideInvert}
        x={$coordsOutsideInvert.x - $sizeOutsideInvert.width / 2}
        y={$coordsOutsideInvert.y - $sizeOutsideInvert.height / 2}
        rx={$borderRadiusOutsideInvert}
        ry={$borderRadiusOutsideInvert}
        width={$sizeOutsideInvert.width}
        height={$sizeOutsideInvert.height}
      />
      <rect
        class="inside"
        fill={"#ffffff"}
        fill-opacity={isFullScreen ? $fillOpacityInsideInvert : 0}
        stroke={isLocked && isFullScreen ? "#ffffff" : "transparent"}
        stroke-width={isLocked ? "2px" : "0"}
        stroke-opacity={isFullScreen && $strokeOpacityInsideInvert}
        x={$coordsInsideInvert.x - $sizeInsideInvert.width / 2}
        y={$coordsInsideInvert.y - $sizeInsideInvert.height / 2}
        rx={$borderRadiusInsideInvert}
        ry={$borderRadiusInsideInvert}
        width={$sizeInsideInvert.width}
        height={$sizeInsideInvert.height}
      />
    </svg>
  </div>
{/if}

<style>
  div {
    overflow: hidden;
    position: fixed;
    pointer-events: none;
    top: 0;
    left: 0;
    z-index: 99;
    width: 100%;
    height: 100%;
  }
  .disable-pointer {
    pointer-events: unset;
  }
  svg {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    margin: 0;
  }
  /* rect.inside {
    stroke-opacity: 0.8;
  }
  rect.outside {
    stroke-opacity: 0.25;
  } */
  .invert {
    z-index: 9999;
  }
</style>
