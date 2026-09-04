# CEFR Writing Skill Assessment

Assess user language writing ski to the Common European Framework of Reference (CEFR) for Languages.

## CEFR Proficiency Levels

###  A (Basic User):
- A1 (Breakthrough): "I can understand and use familiar everyday expressions"
- A2 (Waystage): "I can communicate in simple and routine tasks"

### B (Independent User):
- B1 (Threshold): "I can deal with most situations while travelling"
- B2 (Vantage): "I can interact with a degree of fluency and spontaneity"

### C (Proficient User):
- C1 (Effective Operational Proficiency): "I can express ideas fluently and spontaneously"
- C2 (Mastery): "I can understand with ease virtually everything"


## Examples by Level

### C1 Writing:

- Can express ideas fluently in clear, well-structured text.
- Can write complex letters, reports, or articles.

## Assessment Design - CEFR-Aligned Rubrics

- Fluency and coherence
- Grammatical range and accuracy
- Lexical resource
- Task achievement

## Output

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "EssayEvaluationReport",
  "type": "object",
  "properties": {
    "band": { "type": "integer" },
    "cefr": { "type": "string" },
    "breakdown": {
      "type": "object",
      "additionalProperties": { "$ref": "#/$defs/CriterionBreakdown" }
    },
    "tags": { "$ref": "#/$defs/Tags" },
    "focus": { "$ref": "#/$defs/Focus" },
    "n_words": { "type": "integer" },
    "n_original_words": { "type": "integer" },
    "rubric": { "type": "string" },
    "cminor_version": { "type": "string" },
    "allowed_remaining": { "$ref": "#/$defs/AllowedRemaining" }
  },
  "required": [
    "band",
    "cefr",
    "breakdown",
    "tags",
    "focus",
    "n_words",
    "n_original_words",
    "rubric",
    "cminor_version",
    "allowed_remaining"
  ],
  "$defs": {
    "ValueList": {
      "type": "object",
      "properties": {
        "values": {
          "type": "array",
          "items": { "type": "integer" }
        }
      },
      "required": ["values"]
    },
    "ValueConstantList": {
      "type": "object",
      "properties": {
        "values": {
          "type": "array",
          "items": { "type": "number" }
        },
        "constants": {
          "type": "array",
          "items": { "type": "number" }
        }
      },
      "required": ["values", "constants"]
    },
    "LevelStats": {
      "type": "object",
      "properties": {
        "fit_curve": {
          "type": "array",
          "items": { "type": "number" }
        },
        "ninety_five": {
          "type": "array",
          "items": { "type": "number" }
        },
        "fit_error": {
          "type": "array",
          "items": { "type": "number" }
        }
      },
      "required": ["fit_curve", "ninety_five", "fit_error"]
    },
    "VocabularyStats": {
      "type": "object",
      "properties": {
        "sum_token": { "$ref": "#/$defs/ValueList" },
        "cumsum_token": { "$ref": "#/$defs/ValueConstantList" },
        "sum_type": { "$ref": "#/$defs/ValueList" },
        "cumsum_type": { "$ref": "#/$defs/ValueConstantList" },
        "level": { "$ref": "#/$defs/LevelStats" }
      },
      "required": ["sum_token", "cumsum_token", "sum_type", "cumsum_type", "level"]
    },
    "SentenceDetail": {
      "type": "object",
      "properties": {
        "id": { "type": "array", "items": { "type": "integer" } },
        "word": { "type": "array", "items": { "type": "string" } },
        "lemma": { "type": "array", "items": { "type": "string" } },
        "pos": { "type": "array", "items": { "type": "string" } },
        "whitespace": { "type": "array", "items": { "type": "boolean" } },
        "weight": { "type": "array", "items": { "type": "number" } },
        "CEFR_vocabulary": { "type": "array", "items": { "type": "integer" } },
        "form": { "type": "array", "items": { "type": "string" } },
        "tense1": { "type": "array", "items": { "type": "string" } },
        "tense2": { "type": "array", "items": { "type": "string" } },
        "CEFR_tense": { "type": "array", "items": { "type": "number" } },
        "tense_span": {
          "type": "array",
          "items": {
            "type": "array",
            "items": { "type": "integer" }
          }
        },
        "clause_form": { "type": "array", "items": { "type": "string" } },
        "clause": { "type": "array", "items": { "type": "string" } },
        "clause_span": {
          "type": "array",
          "items": {
            "type": "array",
            "items": { "type": "integer" }
          }
        },
        "CEFR_clause": { "type": "array", "items": { "type": "integer" } },
        "CEFR_sentence": { "type": "number" }
      },
      "required": [
        "id", "word", "lemma", "pos", "whitespace", "weight", "CEFR_vocabulary",
        "form", "tense1", "tense2", "CEFR_tense", "tense_span", "clause_form",
        "clause", "clause_span", "CEFR_clause", "CEFR_sentence"
      ]
    },
    "CriterionBreakdown": {
      "type": "object",
      "properties": {
        "band": { "type": "integer" },
        "breakdown": {
          "type": "object",
          "additionalProperties": { "type": "integer" }
        },
        "raw": { "type": "object" },
        "comment": { "type": "string" },
        "name": { "type": "string" },
        "stats": { "$ref": "#/$defs/VocabularyStats" },
        "sentences": {
          "type": "object",
          "additionalProperties": { "$ref": "#/$defs/SentenceDetail" }
        }
      },
      "required": ["band", "breakdown", "raw", "comment", "name"]
    },
    "TagDetail": {
      "type": "object",
      "properties": {
        "id": { "type": "string" },
        "content": { "type": "string" },
        "comment": { "type": "string" },
        "revision": { "type": "string" },
        "type": { "type": "string" },
        "band": { "type": "integer" },
        "combined_tagged": { "type": "string" }
      },
      "required": ["id", "content", "comment", "revision", "type", "band", "combined_tagged"]
    },
    "InaccuracyDetail": {
      "type": "object",
      "properties": {
        "content": { "type": "string" },
        "revision": { "type": "string" },
        "comment": { "type": "string" },
        "type": { "type": "string" },
        "band": { "type": "integer" },
        "id": { "type": "string" },
        "combined_tagged": { "type": "string" }
      },
      "required": ["content", "revision", "comment", "type", "band", "id", "combined_tagged"]
    },
    "LrGrDetail": {
      "type": "object",
      "properties": {
        "sentence": { "type": "string" },
        "inaccuracies": {
          "type": "array",
          "items": { "$ref": "#/$defs/InaccuracyDetail" }
        }
      },
      "required": ["sentence", "inaccuracies"]
    },
    "Tags": {
      "type": "object",
      "properties": {
        "tr": { "type": "string" },
        "tr_details": {
          "type": "array",
          "items": { "$ref": "#/$defs/TagDetail" }
        },
        "cc": { "type": "string" },
        "cc_details": {
          "type": "array",
          "items": { "$ref": "#/$defs/TagDetail" }
        },
        "lr": { "type": "string" },
        "lr_details": {
          "type": "array",
          "items": { "$ref": "#/$defs/TagDetail" }
        },
        "gr": { "type": "string" },
        "gr_details": {
          "type": "array",
          "items": { "$ref": "#/$defs/TagDetail" }
        },
        "lr_gr": { "type": "string" },
        "lr_gr_details": {
          "type": "array",
          "items": { "$ref": "#/$defs/LrGrDetail" }
        }
      },
      "required": [
        "tr", "tr_details", "cc", "cc_details", "lr", "lr_details",
        "gr", "gr_details", "lr_gr", "lr_gr_details"
      ]
    },
    "Focus": {
      "type": "object",
      "properties": {
        "category": { "type": "string" },
        "title": { "type": "string" },
        "explanation": { "type": "string" }
      },
      "required": ["category", "title", "explanation"]
    },
    "AllowedRemaining": {
      "type": "object",
      "properties": {
        "remaining_coins": { "type": "number" },
        "max_coins": { "type": "number" },
        "next_refill": { "type": "integer" }
      },
      "required": ["remaining_coins", "max_coins", "next_refill"]
    }
  }
}

```
