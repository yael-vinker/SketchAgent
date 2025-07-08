
# SketchAgent: Language-Driven Sequential Sketch Generation

<a href="https://yael-vinker.github.io/sketch-agent/"><img src="https://img.shields.io/static/v1?label=Project&message=Website&color=blue"></a>
<a href="https://arxiv.org/abs/2411.17673"><img src="https://img.shields.io/badge/arXiv-2311.13608-b31b1b.svg"></a>
<a href="https://www.apache.org/licenses/LICENSE-2.0.txt"><img src="https://img.shields.io/badge/License-Apache-yellow"></a>

<br>
<p align="center">
<img src="repo_images/teaser.jpg" width="90%"/>  
  
> <a href="">**SketchAgent: Language-Driven Sequential Sketch Generation**</a>
>
<a href="https://yael-vinker.github.io/website/" target="_blank">Yael Vinker</a>,
<a href="https://tamarott.github.io/" target="_blank">Tamar Rott Shaham</a>,
<a href="https://kristinezheng.github.io/" target="_blank">Kristine Zheng</a>,
<a href="https://www.linkedin.com/in/alex-zhao-a28b12176/" target="_blank">Alex Zhao</a>,
<a href="https://profiles.stanford.edu/judith-fan" target="_blank">Judith E Fan</a>,
<a href="https://groups.csail.mit.edu/vision/torralbalab/" target="_blank">Antonio Torralba</a>

> <br>
>  SketchAgent leverages an off-the-shelf multimodal LLM to facilitate language-driven, sequential sketch generation through an intuitive sketching language. It can sketch diverse concepts, engage in interactive sketching with humans, and edit content via chat.
</p>

## Setup
Clone the repository and navigate to the project folder:
```
git clone https://github.com/yael-vinker/SketchAgent.git
cd SketchAgent
```
Set up the environment:
```
conda env create -f environment.yml
conda activate sketch_agent
```

**For Mac users**, use the following environment file instead:
```
conda env create -f mac_environment.yml
conda activate sketch_agent
```
If python flashes a warning at you, try reinstalling `cairosvg`:
```
conda uninstall cairosvg && conda install cairosvg
```

#### API Key
This repository requires an Anthropic API key. If you don't have one, [create an Anthropic account](https://console.anthropic.com/login) and follow the instructions to obtain a key.

Once you have the key, save it in the ```.env``` file:
```
ANTHROPIC_API_KEY=<your_key>
```

If you want to use the `gpt-4o` model, you will also need an OpenAI API key. You can get one from the [OpenAI website](https://beta.openai.com/signup/). Once you have the key, add it to your `.env` file:
```
OPENAI_API_KEY=<your_key>
```

# Start Sketching! :woman_artist: :art:
## Text-to-Sketch
Generate a single sketch by running:
```
python gen_sketch.py --concept_to_draw "<your_concept_here>" 
```
For example:
```
python gen_sketch.py --concept_to_draw "sailboat" 
```

Optional arguments:
* ```--model``` Default is ```"claude-3-5-sonnet-20240620"```. Set to ```"gpt-4o"``` to use the OpenAI model.
* ```--seed_mode``` Default is ```"deterministic"``` for reproducible results. Set to ```"stochastic"``` for increased variability.
* ```--path2save``` By default, results are saved to ```results/test/```.

## Collaborative Sketching
Collaborate with SketchAgent by alternating strokes! 
To use the interactive interface:
```
python collab_sketch.py
```
This will launch a Flask-based web application. Once running, look for the following output in the terminal:
```
Server running at: http://<your-ip-address>:5000
```
Open the provided URL in your web browser to interact with the application. Results are saved to ```results/collab_sketching/```.
Use the text box to change the concept to be drawn.

## Chat-Based Editing

<br>
<p align="center">
<img src="repo_images/interface.png" width="90%"/>  

Interact with SketchAgent through natural language to edit existing sketches! To use the chat-based editing interface:

```bash
python chat_and_edit.py
```

This will launch a Flask-based web application. Once running, look for output like:

```
Server running at: http://<your-ip-address>:5000
```

You can then:

* Give **textual instructions** to edit specific sketch elements
* Add new elements through **natural conversation**

Results are saved to:

```
results/api_{timestamp}_{session_id}
```

---

### 🧑‍💻 Accessing the Interface

#### ✅ If Running Locally:

Open the printed URL (e.g., `http://127.0.0.1:5000`) in your browser.

#### 🔐 If Running Remotely via SSH:

Use **SSH port forwarding** to access the app from your local browser:

1. On your local machine (not the server), forward the port:

   ```bash
   ssh -L 5000:localhost:5000 your_username@remote_server_ip
   ```

2. Once connected and the app is running, open:

   ```
   http://localhost:5000
   ```

   in your local browser. This securely tunnels traffic to the remote Flask app.




## Tips:
* The ```gen_sketch.py``` script produces sketches with variability. Try running it multiple times to explore different outcomes.
* Prompts are available in the ```prompts.py file```. For unique concepts, ensure that your input prompt is clear and meaningful.

## TODOs

- [ ] Add support for chat based editing.
- [ ] Add SVG drawing process animations in HTML.
- [ ] Add support of other backbone models (GPT4o, LLama3).

## Citation
If you find this useful for your research, please cite the following:
```bibtex
@misc{vinker2024sketchagent,
      title={SketchAgent: Language-Driven Sequential Sketch Generation}, 
      author={Yael Vinker and Tamar Rott Shaham and Kristine Zheng and Alex Zhao and Judith E Fan and Antonio Torralba},
      year={2024},
      eprint={2411.17673},
      archivePrefix={arXiv},
      primaryClass={cs.CV},
      url={https://arxiv.org/abs/2411.17673}, 
}
```
