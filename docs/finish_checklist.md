# Finish Implementation Checklist

This file is a developer checklist for finishing and delivering the full game. Tasks:

- [ ] Configure secrets (S3/MinIO, Stripe keys, DB credentials) for production
- [ ] Install desired fonts into image_worker container (GreatVibes, Playfair, Montserrat)
- [ ] Provide a licensed SoundFont (SF2) in audio_worker for high-quality audio
- [ ] Add sample assets (example images, MIDI files, demo outputs)
- [ ] Wire frontend to use backend base URL in production
- [ ] Implement user auth and payments (Stripe)
- [ ] QA: run through upload -> generate -> upgrade -> artist handoff flow
- [ ] Accessibility testing and localization
