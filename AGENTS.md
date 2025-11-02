# Haiku Creation Swarm - Agent Directory

## Communication Protocol (MANDATORY)
Every agent MUST introduce themselves with this exact format:
"I am the [Agent_Name] agent from the [folder_name] folder. I am contacting you because [reason]. I need you to [request]. Please respond with [format]."

## Available Agents & Their Roles

### 1. Haiku Coordinator (haiku-coordinator folder)
- **Port**: 3001
- **Role**: Coordinates the creation of haikus across multiple languages and ensures thematic consistency
- **Contact for**: Overall coordination, final haiku compilation, theme decisions

### 2. Poetry Translator (poetry-translator folder)
- **Port**: 3002
- **Role**: Translates and adapts haikus between languages while maintaining poetic structure and meaning
- **Contact for**: Translation requests, syllable count verification, linguistic accuracy

### 3. Theme Synchronizer (theme-synchronizer folder)
- **Port**: 3003
- **Role**: Ensures thematic consistency across all haikus and coordinates the narrative thread
- **Contact for**: Theme development, imagery coordination, narrative consistency

### 4. Quality Reviewer (quality-reviewer folder)
- **Port**: 3004
- **Role**: Reviews haikus for structural correctness, poetic quality, and adherence to haiku principles
- **Contact for**: Quality assessment, structural validation, final approval

### 5. Cultural Advisor (cultural-advisor folder)
- **Port**: 3005
- **Role**: Ensures cultural appropriateness and authenticity of haikus across different languages and cultures
- **Contact for**: Cultural guidance, symbolism advice, cultural sensitivity checks

## Swarm Workflow

1. **Initial Theme Selection**: Theme Synchronizer proposes themes to Cultural Advisor for validation
2. **Cultural Validation**: Cultural Advisor validates themes and suggests culturally appropriate imagery
3. **Haiku Creation**: Haiku Coordinator works with Poetry Translator to create initial haikus
4. **Quality Review**: Quality Reviewer validates structure and poetic quality
5. **Final Coordination**: Haiku Coordinator ensures all haikus work together thematically

## Inter-Agent Communication Rules

- **ALL communication must follow the protocol exactly**
- **No direct agent-to-agent communication without proper introduction**
- **Orchestrator (port 3000) enforces all communication rules**
- **Document all communication for final coordination**

## Success Criteria

- 5 haikus completed in 5 different languages
- All haikus maintain 5-7-5 syllable structure
- Thematic consistency across all haikus
- Cultural appropriateness validated
- High poetic quality achieved