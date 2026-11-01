# NeuroScreen Streamlit dashboard

Phase 1-5 feature-extraction dashboard. It accepts:

- **One child:** any number of video/audio recordings for one child.
- **Multiple children:** any number of recordings, with each file assigned to a de-identified child ID.

For every uploaded video it runs: EfficientNet-B0 emotion probabilities (Phase 1),
ResNet50 class probabilities (Phase 2), MediaPipe Pose plus the Phase 3 LSTM, and
the Phase 4 audio pipeline. It aggregates all recordings belonging to a child into
one feature row. The four displayed domain scores are transparent **prototype
composites**, not Phase 6 XGBoost scores and not diagnoses.

## Run locally

```powershell
py -m pip install -r requirements.txt
streamlit run app.py
```

Keep these checkpoint files in the same directory as `app.py`:

- `emotion_controlled_finetune_best.pth`
- `autism_face_best.pth`
- `behavior_group_best.pth`

## Streamlit Community Cloud

1. Create a private GitHub repository. Do not upload identifiable child recordings.
2. Add `app.py`, `feature_extractors.py`, `requirements.txt`, `packages.txt`, and the
   three checkpoint files. For checkpoints over GitHub's normal file-size limit, use
   Git LFS or place them in a private object store and adapt the loader.
3. Visit https://share.streamlit.io, connect the repository, select `app.py`, and deploy.
4. Test with short, non-identifiable demo media. Free hosting can sleep and may not
   have enough memory/CPU for Whisper and three PyTorch models simultaneously.

The Phase-5 UI deliberately accepts only project-level numeric domain inputs and
does not reproduce M-CHAT-R/F wording.
