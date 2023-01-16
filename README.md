# HordeAutoWebWorker
# [hordeautowebworker.github.io](https://hordeautowebworker.github.io)

A Javascript based Stable Horde Worker bridging Automatic1111 API with Stable Horde API that runs **entirely in browser**. No Python, no extra 20 GB downloads or duplicate installs, just click and share your own local models.
Unlike the existing Automatic1111 extension, this worker supports hosting multiple selected models together, and does the switching for you. It also attempts to automatically determine the name of the models you have based on filename (see caveat 3).

Caveats: 
1. Although the user can express a preference to avoid nsfw, it cannot be guaranteed as this worker runs entirely from the web, it cannot (and should not) download/install new models for the user, and without CompVis stable-diffusion-safety-checker it means it will not have a NSFW filter. 
2. As we are running from browser, accessing/uploading to R2 buckets may present an issue with CORS restrictions, since it's on different domains. To avoid this headache, we just use bridge_version 7 and support only b64 *for now*. 
3. The .ckpt filenames many A1111 users use may have different filenames from the "official" horde model names. Since calculating hashes on file system is not possible in browser, plus many people use different variants of the same model (fp16/32/pruned), I match them via db.json list of ckpt filenames instead. As this may have inaccuracies, I've also added a way for users to rename their local model identifiers based on the list of models from horde.
4. API documentation is limited, I have tried to make this as standards compliant as possible, so let me know if something is not right. To aid debugging, this worker uses client_agent = "HordeAutoWebWorker:1" so any misbehavior can be monitored and reported.

Do give it a try and let me know. It's fully open source so feel free to look, but if anyone has concerns I'd suggest using a different API key for peace of mind.