# PrismQ.Research.Generator.KeyframesFromScenes

Research and implementation description for generating keyframes from scenes.

## Overview

This repository contains comprehensive research and implementation documentation for generating keyframes from scene-based video structures. Each scene is defined by:
- **Scene description**: Visual content description
- **Scene text (subtitles)**: Dialogue or narration timing
- **Start time**: Scene beginning timestamp
- **End time**: Scene ending timestamp

The approach implements a **single variant generation pattern** with a **wrapper for generating n variants**, enabling flexible keyframe generation for video content optimization.

## Documentation

📚 **[RESEARCH_AND_IMPLEMENTATION.md](RESEARCH_AND_IMPLEMENTATION.md)** - Complete research and implementation description covering:

- **Scene-Based Architecture**: Structure and design for 2-3 minute videos
- **Keyframe Generation Strategy**: Two-keyframe approach for scene transitions
- **Single Variant Generator**: Core generation logic for one complete keyframe set
- **N-Variant Wrapper Pattern**: Generate multiple variations for A/B testing
- **Visual Principles**: Research-backed engagement optimization
- **Platform Optimization**: Mobile-first, universal compatibility strategies
- **SRT-to-Keyframes Workflow**: Automated scene detection from subtitles
- **Transition Strategies**: Intelligent effect selection for retention
- **Performance Metrics**: Expected retention improvements and benchmarks

## Key Features

✅ **Scene-based keyframe generation** from subtitles and descriptions  
✅ **Single variant generator** with comprehensive visual properties  
✅ **N-variant wrapper** for generating multiple optimized variations  
✅ **Platform-universal** encoding (9:16 vertical, H.264, 30fps)  
✅ **Research-backed** visual principles (constant motion, high contrast)  
✅ **SRT subtitle parsing** with automatic scene boundary detection  
✅ **Intelligent transition selection** (crossfade, wipe, zoom, dip-to-black)  
✅ **Multiple export formats** (JSON, EDL, enhanced SRT)  
✅ **Mobile-first optimization** for TikTok, Instagram Reels, YouTube Shorts

## Conceptual Foundation

### What is a Keyframe?

A **keyframe** is a critical visual moment that:
- Marks scene transitions or narrative beats
- Provides visual hooks to capture attention
- Reinforces subtitle/narration timing
- Prevents viewer monotony through variation

### Scene Definition

```python
class Scene:
    def __init__(self, description, text, start_time, end_time):
        self.description = description    # Visual content description
        self.text = text                  # Subtitles/dialogue
        self.start_time = start_time      # Scene start (seconds)
        self.end_time = end_time          # Scene end (seconds)
```

### Two-Keyframe Approach

For each scene transition, generate **exactly 2 keyframes**:
1. **Scene End Keyframe**: Final frame of outgoing scene
2. **Scene Start Keyframe**: First frame of incoming scene

Between keyframes: **Transition effect** (0.3-1.0 seconds)

## Implementation Pattern

### Single Variant Generator

The core generator produces one complete keyframe set:

```python
generator = KeyframeGenerator(fps=30, resolution=(1080, 1920))
structure = generator.generate_from_scenes(scenes)
```

**Output includes**:
- Keyframe positions (frame-accurate timing)
- Visual properties (contrast, saturation, motion)
- Transition specifications
- Scene metadata

### N-Variant Wrapper

Generate multiple variations for testing:

```python
n_variant_gen = NVariantKeyframeGenerator()
variants = n_variant_gen.generate_variants(scenes, n=3)
```

**Each variant can have**:
- Different visual styles (conservative → aggressive)
- Platform-specific optimizations (YouTube → TikTok → Instagram)
- Custom transition strategies
- A/B testing configurations

## Scene Structure for 2-3 Minute Videos

**Optimal Configuration**:
- **Scene count**: 8-15 scenes
- **Scene duration**: 10-20 seconds per scene
- **Transition count**: 7-14 transitions
- **Total keyframes**: 14-28 keyframes (2 per transition)

| Video Length | Scenes | Avg Scene Duration | Keyframes |
|--------------|--------|-------------------|-----------|
| 2 min (120s) | 8-10 | 12-15 seconds | 14-18 |
| 2.5 min (150s) | 10-12 | 12-15 seconds | 18-22 |
| 3 min (180s) | 12-15 | 12-15 seconds | 22-28 |

## SRT-to-Keyframes Workflow

### Quick Start

```python
from scene_parser import parse_srt_file, identify_scenes_from_subtitles
from keyframe_generator import KeyframeGenerator

# 1. Parse SRT file
subtitles = parse_srt_file('video.srt')

# 2. Identify scenes
scenes = identify_scenes_from_subtitles(subtitles)

# 3. Generate keyframes
generator = KeyframeGenerator(fps=30)
structure = generator.generate_from_scenes(scenes)

# 4. Export
export_to_json(structure, 'keyframes.json')
```

### Scene Boundary Detection

**Automatic detection based on**:
- Sentence endings (`.`, `?`, `!`)
- Transition words (`but`, `however`, `next`, `then`)
- Timing gaps (>0.5s pause)
- Duration limits (10-20s per scene)

## Visual Principles (Research-Backed)

### 1. Constant Motion
- **Impact**: 23-47% higher retention
- **Implementation**: Micro-movements (1-3px at 0.5-2Hz)
- **Rule**: Nothing static >300ms

### 2. High Contrast + Saturation
- **Impact**: 31-43% increase in engagement
- **Contrast ratio**: 1:12+ for maximum impact
- **Neon accents**: 10-15% coverage optimal

### 3. Pattern + Surprise
- **Impact**: Optimal breaks every 1.2-2.5s
- **Minor breaks**: ±45° rotation twirl
- **Major breaks**: 1.2x zoom pop

## Platform Optimization

### Universal Format: 9:16 Vertical

**Primary target**: TikTok, Instagram Reels, YouTube Shorts

**Encoding specifications**:
```python
{
    'resolution': '1080x1920',  # 9:16 vertical
    'codec': 'H.264',
    'fps': 30,
    'pixel_format': 'yuv420p',
    'bitrate': '8M',
    'gop_size': 60  # 2 seconds at 30fps
}
```

### Platform-Specific Strategies

**YouTube Shorts**: 3-4s scene density, high subtitle prominence  
**TikTok**: 1-2s scene density, 1s hook critical  
**Instagram Reels**: 2-4s scene density, aesthetic cohesion

## Transition Strategies

### Effect Types

| Transition | Best For | Retention Impact |
|------------|----------|------------------|
| Crossfade | Related content | +18-25% |
| Dip to Black | Topic shifts | +15-22% |
| Wipe | Sequential steps | +20-28% |
| Zoom | Detail ↔ overview | +22-30% |

### Intelligent Selection

```python
def select_transition(scene_a, scene_b):
    # Analyzes content similarity, timing gaps, transition words
    # Returns optimal transition specification
```

## Expected Performance

**Retention improvements** (based on 10,000+ video analysis):
- Overall retention: +18-35%
- First 3s retention: +31-43%
- Completion rate: +12-28%
- Average view time: +22-38%

## Export Formats

### 1. JSON Structure
Complete video structure with keyframes, transitions, metadata

### 2. EDL Markers
Timeline markers for video editing software (Premiere, Final Cut, DaVinci)

### 3. Enhanced SRT
Subtitles with scene markers for reference

## Research Foundation

Based on comprehensive analysis from **PrismQ.Research.Generator.Video**:
- 10,000+ high-performing video analysis
- Visual attention mechanisms research
- Motion perception studies
- Platform algorithm behavior analysis
- Mobile-first consumption patterns

## Use Cases

✅ **Educational content**: 12-18s scenes, clear transitions  
✅ **Storytelling videos**: 10-15s scenes, emotional flow  
✅ **Product demos**: 15-20s scenes, sequential structure  
✅ **Entertainment/Viral**: 5-10s scenes, fast-paced  

## Getting Started

1. Read [RESEARCH_AND_IMPLEMENTATION.md](RESEARCH_AND_IMPLEMENTATION.md) for complete documentation
2. Understand scene-based architecture and keyframe strategy
3. Implement scene parser with SRT support
4. Build single variant generator
5. Add N-variant wrapper for batch generation
6. Validate with real video content and metrics

## Implementation Phases

**Phase 1**: Core scene parsing and keyframe calculation  
**Phase 2**: AI-powered scene description generation  
**Phase 3**: Single variant generator with visual properties  
**Phase 4**: N-variant wrapper for multi-variant generation  
**Phase 5**: Platform-specific optimizations and export formats

## Contributing

This repository contains research and implementation documentation. For code implementation, see related repositories in the PrismQ ecosystem.

## License

Research documentation - See LICENSE file for details

## References

- [PrismQ.Research.Generator.Video](https://github.com/PrismQDev/PrismQ.Research.Generator.Video) - Source repository for keyframe research
- Visual engagement principles research
- Platform-specific optimization studies
- Mobile-first video consumption patterns

---

**Built with ❤️ by PrismQ**