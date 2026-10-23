# References

Sources were checked on 23 October 2026. The register contains 35 sources, including eleven scientific publications. S35 is project evidence, not an independent scientific study. Product/model cards describe documented capabilities rather than Hattama benchmark results.

## S01

Mussakhojayeva, S., Khassanov, Y., and Varol, H. A. (2022). KSC2: An Industrial-Scale Open-Source Kazakh Speech Corpus. Interspeech 2022, 1367–1371.

https://www.isca-archive.org/interspeech_2022/mussakhojayeva22_interspeech.html

Use in this project: Kazakh speech and code-switching; informs ASR development data, not meeting-summary ground truth.

## S02

Radford, A., et al. (2023). Robust Speech Recognition via Large-Scale Weak Supervision. ICML, PMLR 202, 28492–28518.

https://proceedings.mlr.press/v202/radford23a

Use in this project: Multilingual ASR starting point; local language and recording conditions still require measurement.

## S03

Bain, M., Huh, J., Han, T., and Zisserman, A. (2023). WhisperX: Time-Accurate Speech Transcription of Long-Form Audio. Interspeech 2023.

https://www.isca-archive.org/interspeech_2023/bain23_interspeech.html

Use in this project: Long audio segmentation and alignment; Kazakh alignment availability must be checked.

## S04

Bredin, H. (2023). pyannote.audio 2.1 speaker diarization pipeline: principle, benchmark, and recipe. Interspeech 2023, 1983–1987.

https://www.isca-archive.org/interspeech_2023/bredin23_interspeech.html

Use in this project: Speaker clustering motivates editable anonymous labels and a separate diarization evaluation.

## S05

Zhong, M., et al. (2021). QMSum: A New Benchmark for Query-based Multi-domain Meeting Summarization. NAACL, 5905–5921.

https://aclanthology.org/2021.naacl-main.472/

Use in this project: Locate relevant discussion before summarization; English benchmark does not establish bilingual quality.

## S06

Kim, H., Cho, M., and Na, S.-H. (2023). ExplainMeetSum: A Dataset for Explainable Meeting Summarization Aligned with Human Intent. ACL, 13079–13098.

https://aclanthology.org/2023.acl-long.731/

Use in this project: Evidence-aligned summaries motivate source segment links and review.

## S07

Hu, Y., et al. (2023). MeetingBank: A Benchmark Dataset for Meeting Summarization. ACL, 16409–16423.

https://aclanthology.org/2023.acl-long.906/

Use in this project: Long meeting transcripts and professional minutes inform chunking and structured output.

## S08

Fabbri, A. R., et al. (2021). SummEval: Re-evaluating Summarization Evaluation. TACL 9, 391–409.

https://aclanthology.org/2021.tacl-1.24/

Use in this project: Human evaluation complements automatic overlap metrics; news-domain findings need cautious transfer.

## S09

Kirstein, F., Ruas, T., and Gipp, B. (2025). What’s Wrong? Refining Meeting Summaries with LLM Feedback. COLING, 2100–2120.

https://aclanthology.org/2025.coling-main.143/

Use in this project: Meeting error analysis motivates explicit checks for omissions, unsupported claims and wrong attribution.

## S10

Kirstein, F., Ruas, T., and Gipp, B. (2025). Is my Meeting Summary Good? Estimating Quality with a Multi-LLM Evaluator. COLING Industry Track, 561–574.

https://aclanthology.org/2025.coling-industry.48/

Use in this project: Model-based evaluation is an auxiliary signal; bilingual human adjudication remains the reference.

## S11

Fireflies.ai. Supported languages.

https://guide.fireflies.ai/articles/2973706448

Use in this project: Kazakh and Russian are listed for transcription and summaries; exact mixed-pair quality is unverified.

## S12

Fireflies.ai. How to upload and transcribe audio or video files.

https://guide.fireflies.ai/articles/3893959957-how-to-upload-and-transcribe-audio-or-video-files-in-fireflies

Use in this project: Upload, transcript, summary and action-item workflow supports competitor comparison.

## S13

Notta. What languages does Notta support?

https://support.notta.ai/hc/en-us/articles/4403155631131-What-languages-does-Notta-support

Use in this project: Russian appears in transcription lists; Kazakh appears as a translation target, which is not ASR support.

## S14

Notta. Bilingual transcription and translation on the web.

https://support.notta.ai/hc/en-us/articles/23437010425755-Bilingual-transcription-translation-Web

Use in this project: Uploaded and live bilingual workflows; the listed source languages do not include Kazakh.

## S15

Notta. Edit, regenerate or delete AI Notes.

https://support.notta.ai/hc/en-us/articles/37290499079835-Edit-Regenerate-or-Delete-AI-Notes

Use in this project: Editable AI notes and tasks inform comparison of correction workflows.

## S16

Notta. Export AI summaries.

https://support.notta.ai/hc/en-us/articles/37290527491739-Export-AI-summaries

Use in this project: Documented notes export, subject to access and plan conditions.

## S17

Otter.ai. Supported languages.

https://help.otter.ai/hc/en-us/articles/360047247414-Supported-languages

Use in this project: The published transcription list does not include Kazakh or Russian.

## S18

Otter.ai. What is Otter?

https://help.otter.ai/hc/en-us/articles/360035266494-What-is-Otter

Use in this project: Import, editing, sharing and export workflows.

## S19

Otter.ai. Meeting Summary Overview.

https://help.otter.ai/hc/en-us/articles/9156381229079-Meeting-Summary-Overview

Use in this project: Meeting summaries and action items are established competitor features.

## S20

OpenAI. Whisper repository and model information.

https://github.com/openai/whisper

Use in this project: Multilingual transcription candidates; pin model revision and decoding settings.

## S21

Qwen team. Qwen3-4B-Instruct-2507 model card.

https://huggingface.co/Qwen/Qwen3-4B-Instruct-2507

Use in this project: Upstream model for the current quantized local generator; model context is not the application context limit.

## S22

FastAPI. Features.

https://fastapi.tiangolo.com/features/

Use in this project: Typed API schemas and documented interfaces for the Python model pipeline.

## S23

Celery. Introduction.

https://docs.celeryq.dev/en/stable/getting-started/introduction.html

Use in this project: Dedicated background workers with a broker; application must enforce idempotency.

## S24

PostgreSQL. Transaction isolation.

https://www.postgresql.org/docs/current/transaction-iso.html

Use in this project: Transactional revision and approval checks; concurrency policies require explicit design.

## S25

JetBrains. Import from CSV in YouTrack Cloud.

https://www.jetbrains.com/help/youtrack/cloud/import-from-csv.html

Use in this project: Current CSV workflow uses Google Sheets as an intermediary; manual task creation is an alternative.

## S26

Zoom. Add Realtime Media Streams to your app.

https://developers.zoom.us/docs/rtms/meetings/add-features/

Use in this project: Audio-only authorised live connector requires app scopes, events and Developer Pack credits.

## S27

Google. Get started with Meet Media API.

https://developers.google.com/workspace/meet/media-api/guides/get-started

Use in this project: Current preview access constraints support deferring this connector.

## S28

Chen, Z., Futian, J., Deng, Y., He, C., and Li, B. (2025). Meetalk: Retrieval-Augmented and Adaptively Personalized Meeting Summarization with Knowledge Learning from User Corrections. KnowFM.

https://aclanthology.org/2025.knowllm-1.9/

Use in this project: Published user-study rationale for correction and review; not interviews conducted by our team.

## S29

Meta. Llama 3.1 8B Instruct model card.

https://huggingface.co/meta-llama/Llama-3.1-8B-Instruct

Use in this project: Comparison candidate; Kazakh and Russian are outside the explicitly supported language list.

## S30

Google DeepMind. Gemma 3 12B IT model card.

https://huggingface.co/google/gemma-3-12b-it

Use in this project: Larger multilingual generation candidate; assess resource fit and bilingual minutes quality.

## S31

NVIDIA. Nemotron 3 Nano 30B A3B BF16 model card.

https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Nano-30B-A3B-BF16

Use in this project: MoE comparison candidate; active parameters do not equal stored model size.

## S32

SQLite. Appropriate Uses For SQLite.

https://www.sqlite.org/whentouse.html

Use in this project: Supports embedded local storage; multiwriter server use changes the tradeoff.

## S33

k2 fsa. sherpa onnx Speaker Diarization documentation.

https://k2-fsa.github.io/sherpa/onnx/speaker-diarization/index.html

Use in this project: Segmentation and embedding components used by the local speaker pipeline.

## S34

Serikbay, A. Kazakh Russian Mixed STT model card.

https://huggingface.co/alibiserikbay/kazakh-russian-mixed-stt

Use in this project: Current CTC speech-model provenance; local evaluation is still required.

## S35

Hattama team. Application source and recorded hackathon evidence. Baseline commit 13d2271.

https://github.com/f0nce/hattama/tree/13d2271e846f6566219d8899ac7bf3085865debd

Use in this project: Primary evidence for implemented behavior, architecture, runtime limits and historical measurements.
