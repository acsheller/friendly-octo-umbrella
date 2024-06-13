The gpt based models are not running so need to figure out what is going on.

```.bash
(MPR) sheller@ws-sheller:~/SUBER$ python3 -m ablations.movies.run_gpt --llm-model gpt-3.5-turbo-0613
Running genre_preference_paper
  0%|                                                                                                                                   | 0/8 [00:00<?, ?it/s]
Traceback (most recent call last):
  File "/home/sheller/SUBER/environment/LLM/openai_api.py", line 41, in request_rating_0_9
    out = openai.ChatCompletion.create(
  File "/home/sheller/miniconda3/envs/MPR/lib/python3.9/site-packages/openai/lib/_old_api.py", line 39, in __call__
    raise APIRemovedInV1(symbol=self._symbol)
openai.lib._old_api.APIRemovedInV1: 

You tried to access openai.ChatCompletion, but this is no longer supported in openai>=1.0.0 - see the README at https://github.com/openai/openai-python for the API.

You can run `openai migrate` to automatically upgrade your codebase to use the 1.0.0 interface. 

Alternatively, you can pin your installation to the old version, e.g. `pip install openai==0.28`

A detailed migration guide is available here: https://github.com/openai/openai-python/discussions/742


During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/home/sheller/miniconda3/envs/MPR/lib/python3.9/runpy.py", line 197, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/home/sheller/miniconda3/envs/MPR/lib/python3.9/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/sheller/SUBER/ablations/movies/run_gpt.py", line 67, in <module>
    genre_study.run()
  File "/home/sheller/SUBER/ablations/movies/src/genre_preference_paper.py", line 676, in run
    data_yes, vote_average_tmdb_yes = interact_sequential(
  File "/home/sheller/SUBER/ablations/utils/helper_functions.py", line 29, in interact_sequential
    obs, reward, terminated, _, info = env.step(item)
  File "/home/sheller/SUBER/environment/env.py", line 204, in step
    rating, explanation, html_interaction = self.rating_prompt.query(
  File "/home/sheller/SUBER/environment/LLM/rater.py", line 78, in query
    _, out = self.llm.request_rating_0_9(
  File "/home/sheller/SUBER/environment/LLM/openai_api.py", line 48, in request_rating_0_9
    openai.error.RateLimitError,
AttributeError: module 'openai' has no attribute 'error'

```
