<!--
---
title: "Tagging Strategy"
description: "Controlled vocabulary for document classification and RAG retrieval in desi-quasar-outflows"
author: "VintageDon - https://github.com/vintagedon"
ai_contributor: "Claude Opus 4.5 (Anthropic)"
date: "2025-12-29"
version: "1.0"
tags:
  - domain: documentation
  - type: specification
related_documents:
  - "[Interior README Template](interior-readme-template.md)"
  - "[General KB Template](general-kb-template.md)"
---
-->

# Tagging Strategy

## 1. Purpose

This document defines the controlled tag vocabulary for all documentation in desi-quasar-outflows, enabling consistent classification for human navigation and RAG system retrieval.

---

## 2. Scope

Covers all tag categories, valid values, and usage guidance. Does not cover front-matter field structure—see individual templates for field requirements.

---

## 3. Tag Categories

### Phase Tags

Pipeline execution phases. Documents may belong to multiple phases.

| Tag | Description |
|-----|-------------|
| `phase-01` | Candidate selection (ARD queries, outflow filtering) |
| `phase-02` | Spectral fitting (column density measurements) |
| `phase-03` | Cloudy modeling (photoionization grids) |
| `phase-04` | Energetics derivation (R, Ṁ, Ė_k calculation) |

**Usage**: Tag with all phases a document supports. A methodology doc explaining column density derivation used in phases 02-03 would carry `phase-02`, `phase-03`.

---

### Domain Tags

Primary functional area. Usually one per document.

| Tag | Description |
|-----|-------------|
| `candidate-selection` | ARD queries, outflow identification |
| `spectral-fitting` | Continuum modeling, line measurements |
| `photoionization` | Cloudy modeling, physical conditions |
| `energetics` | Outflow properties, feedback efficiency |
| `validation` | Data quality, fitting QA |
| `documentation` | Methodology, specifications, standards |
| `infrastructure` | Database, storage, compute configuration |

**Usage**: Choose the primary domain. A document about validating spectral fits is `validation`, not `spectral-fitting`.

---

### Type Tags

Document purpose and structure.

| Tag | Description |
|-----|-------------|
| `methodology` | How we do something |
| `reference` | Lookup information (parameter tables, grids) |
| `guide` | Step-by-step procedures |
| `decision-record` | Why we chose X over Y |
| `specification` | Formal requirements |
| `source-code` | Code files and scripts |
| `configuration` | Config files, Cloudy input parameters |
| `data-manifest` | Data inventory and provenance |

**Usage**: One type per document. If a document explains both *how* and *why*, choose the dominant purpose.

---

### Tech Tags

Data sources and external dependencies.

| Tag | Description |
|-----|-------------|
| `desi-dr1` | DESI Data Release 1 base data |
| `ard` | Analysis-Ready Dataset (upstream) |
| `civ-vac` | CIV Absorber Value-Added Catalog |
| `mgii-vac` | MgII Absorber Value-Added Catalog |
| `bhmass-vac` | Black Hole Mass Value-Added Catalog |
| `cloudy` | Cloudy photoionization code |
| `postgresql` | PostgreSQL database |
| `parquet` | Parquet file format |

**Usage**: Tag when the document is specific to that data source or technology. A general methodology doc doesn't need `cloudy`; a doc about Cloudy grid parameters does.

---

### Physics Layer Tags

For analysis-specific documentation.

| Tag | Description |
|-----|-------------|
| `absorber-properties` | Column densities, equivalent widths |
| `physical-conditions` | n_e, N_H, U_H derivation |
| `outflow-energetics` | R, Ṁ, Ė_k, feedback efficiency |

**Usage**: Tag methodology and results documents with the layer(s) they address.

---

## 4. References

| Reference | Link |
|-----------|------|
| Main README | [../../README.md](../../README.md) |
| Interior README Template | [interior-readme-template.md](interior-readme-template.md) |
| General KB Template | [general-kb-template.md](general-kb-template.md) |
| Upstream ARD Schema | [desi-cosmic-void-galaxies ARD Schema](https://github.com/radioastronomyio/desi-cosmic-void-galaxies/blob/main/docs/ARD-SCHEMA-v2.md) |

---
