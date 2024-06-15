
##FIX

do `pip install accelerate -U`

```.bash

(MPR) sheller@ws-sheller:~/SUBER$ python3 -m ablations.movies.run --llm-model TheBloke/Mixtral-8x7B-Instruct-v0.1-GPTQ
╭─────────────────────────────── Traceback (most recent call last) ────────────────────────────────╮
│ /home/sheller/miniconda3/envs/MPR/lib/python3.9/runpy.py:197 in _run_module_as_main              │
│                                                                                                  │
│   194 │   main_globals = sys.modules["__main__"].__dict__                                        │
│   195 │   if alter_argv:                                                                         │
│   196 │   │   sys.argv[0] = mod_spec.origin                                                      │
│ ❱ 197 │   return _run_code(code, main_globals, None,                                             │
│   198 │   │   │   │   │    "__main__", mod_spec)                                                 │
│   199                                                                                            │
│   200 def run_module(mod_name, init_globals=None,                                                │
│                                                                                                  │
│ /home/sheller/miniconda3/envs/MPR/lib/python3.9/runpy.py:87 in _run_code                         │
│                                                                                                  │
│    84 │   │   │   │   │      __loader__ = loader,                                                │
│    85 │   │   │   │   │      __package__ = pkg_name,                                             │
│    86 │   │   │   │   │      __spec__ = mod_spec)                                                │
│ ❱  87 │   exec(code, run_globals)                                                                │
│    88 │   return run_globals                                                                     │
│    89                                                                                            │
│    90 def _run_module_code(code, init_globals=None,                                              │
│                                                                                                  │
│ /home/sheller/SUBER/ablations/movies/run.py:44 in <module>                                       │
│                                                                                                  │
│    41 │   args = parse_args()                                                                    │
│    42 │   name = args.llm_model                                                                  │
│    43 │                                                                                          │
│ ❱  44 │   model = LLM.load_LLM(name)                                                             │
│    45 │                                                                                          │
│    46 │   # During the ablation study we want to look at the raw ratings, not the reward for R   │
│    47 │   args.reward_shaping = "identity"                                                       │
│                                                                                                  │
│ /home/sheller/SUBER/environment/LLM/__init__.py:37 in load_LLM                                   │
│                                                                                                  │
│   34 │   │                                                                                       │
│   35 │   │   return LLMExllama(name)                                                             │
│   36 │   elif name in TRANSFORMERS_MODELS:                                                       │
│ ❱ 37 │   │   from .std_transformers import Transformers                                          │
│   38 │   │                                                                                       │
│   39 │   │   return Transformers(name)                                                           │
│   40                                                                                             │
│                                                                                                  │
│ /home/sheller/SUBER/environment/LLM/std_transformers.py:2 in <module>                            │
│                                                                                                  │
│     1 from typing import Tuple                                                                   │
│ ❱   2 from auto_gptq import exllama_set_max_input_length                                         │
│     3 import torch                                                                               │
│     4 from transformers import (                                                                 │
│     5 │   AutoModelForCausalLM,                                                                  │
│                                                                                                  │
│ /home/sheller/miniconda3/envs/MPR/lib/python3.9/site-packages/auto_gptq/__init__.py:3 in         │
│ <module>                                                                                         │
│                                                                                                  │
│   1 from .modeling import BaseQuantizeConfig                                                     │
│   2 from .modeling import AutoGPTQForCausalLM                                                    │
│ ❱ 3 from .utils.peft_utils import get_gptq_peft_model                                            │
│   4                                                                                              │
│                                                                                                  │
│ /home/sheller/miniconda3/envs/MPR/lib/python3.9/site-packages/auto_gptq/utils/peft_utils.py:9 in │
│ <module>                                                                                         │
│                                                                                                  │
│     6 from typing import List, Optional                                                          │
│     7                                                                                            │
│     8 import torch                                                                               │
│ ❱   9 from peft import get_peft_model, PeftConfig, PeftModel, PeftType                           │
│    10 from peft.peft_model import PEFT_TYPE_TO_MODEL_MAPPING                                     │
│    11 from peft.tuners.lora import LoraConfig, LoraLayer, LoraModel, Embedding                   │
│    12 from peft.tuners.adalora import AdaLoraConfig, AdaLoraLayer, AdaLoraModel                  │
│                                                                                                  │
│ /home/sheller/miniconda3/envs/MPR/lib/python3.9/site-packages/peft/__init__.py:22 in <module>    │
│                                                                                                  │
│   19                                                                                             │
│   20 __version__ = "0.5.0"                                                                       │
│   21                                                                                             │
│ ❱ 22 from .auto import (                                                                         │
│   23 │   AutoPeftModel,                                                                          │
│   24 │   AutoPeftModelForCausalLM,                                                               │
│   25 │   AutoPeftModelForSequenceClassification,                                                 │
│                                                                                                  │
│ /home/sheller/miniconda3/envs/MPR/lib/python3.9/site-packages/peft/auto.py:30 in <module>        │
│                                                                                                  │
│    27 │   AutoModelForTokenClassification,                                                       │
│    28 )                                                                                          │
│    29                                                                                            │
│ ❱  30 from .config import PeftConfig                                                             │
│    31 from .mapping import MODEL_TYPE_TO_PEFT_MODEL_MAPPING                                      │
│    32 from .peft_model import (                                                                  │
│    33 │   PeftModel,                                                                             │
│                                                                                                  │
│ /home/sheller/miniconda3/envs/MPR/lib/python3.9/site-packages/peft/config.py:24 in <module>      │
│                                                                                                  │
│    21 from huggingface_hub import hf_hub_download                                                │
│    22 from transformers.utils import PushToHubMixin                                              │
│    23                                                                                            │
│ ❱  24 from .utils import CONFIG_NAME, PeftType, TaskType                                         │
│    25                                                                                            │
│    26                                                                                            │
│    27 @dataclass                                                                                 │
│                                                                                                  │
│ /home/sheller/miniconda3/envs/MPR/lib/python3.9/site-packages/peft/utils/__init__.py:22 in       │
│ <module>                                                                                         │
│                                                                                                  │
│   19                                                                                             │
│   20 # from .config import PeftConfig, PeftType, PromptLearningConfig, TaskType                  │
│   21 from .peft_types import PeftType, TaskType                                                  │
│ ❱ 22 from .other import (                                                                        │
│   23 │   TRANSFORMERS_MODELS_TO_PREFIX_TUNING_POSTPROCESS_MAPPING,                               │
│   24 │   TRANSFORMERS_MODELS_TO_LORA_TARGET_MODULES_MAPPING,                                     │
│   25 │   TRANSFORMERS_MODELS_TO_ADALORA_TARGET_MODULES_MAPPING,                                  │
│                                                                                                  │
│ /home/sheller/miniconda3/envs/MPR/lib/python3.9/site-packages/peft/utils/other.py:24 in <module> │
│                                                                                                  │
│    21 import accelerate                                                                          │
│    22 import torch                                                                               │
│    23 from accelerate.hooks import add_hook_to_module, remove_hook_from_module                   │
│ ❱  24 from accelerate.utils import is_npu_available, is_xpu_available                            │
│    25                                                                                            │
│    26 from ..import_utils import is_auto_gptq_available                                          │
│    27                                                                                            │
╰──────────────────────────────────────────────────────────────────────────────────────────────────╯
ImportError: cannot import name 'is_npu_available' from 'accelerate.utils' 
(/home/sheller/miniconda3/envs/MPR/lib/python3.9/site-packages/accelerate/utils/__init__.py)
(MPR) sheller@ws-sheller:~/SUBER$ 

```
