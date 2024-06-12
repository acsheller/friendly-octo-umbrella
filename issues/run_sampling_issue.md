When running `python3 abalations.movies.run` it produces the following error:

```.bash
Running sampling_distribution
Traceback (most recent call last):
  File "/home/suber/.conda/envs/MPR/lib/python3.9/runpy.py", line 197, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/home/suber/.conda/envs/MPR/lib/python3.9/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/suber/SUBER/ablations/movies/run.py", line 101, in <module>
    sampling_study.run()
  File "/home/suber/SUBER/ablations/movies/src/sampling.py", line 33, in run
    env = self.create_env()
  File "/home/suber/SUBER/ablations/movies/run.py", line 99, in <lambda>
    lambda: get_enviroment_from_args(model, args), exp_name
  File "/home/suber/SUBER/environment/movies/configs.py", line 291, in get_enviroment_from_args
    items_loader=MoviesLoader(
  File "/home/suber/SUBER/environment/movies/movies_loader.py", line 14, in __init__
    self.data = json.load(json_file)
  File "/home/suber/.conda/envs/MPR/lib/python3.9/json/__init__.py", line 293, in load
    return loads(fp.read(),
  File "/home/suber/.conda/envs/MPR/lib/python3.9/json/__init__.py", line 346, in loads
    return _default_decoder.decode(s)
  File "/home/suber/.conda/envs/MPR/lib/python3.9/json/decoder.py", line 337, in decode
    obj, end = self.raw_decode(s, idx=_w(s, 0).end())
  File "/home/suber/.conda/envs/MPR/lib/python3.9/json/decoder.py", line 355, in raw_decode
    raise JSONDecodeError("Expecting value", s, err.value) from None
json.decoder.JSONDecodeError: Expecting value: line 1 column 1 (char 0)
```

1. Start in `ablations.movies.run` at line 101 which is `sampling_study.run()`
2. got `ablations.movies.src.sampling` line 33 which is `self.create_env()
3. Then to `ablations.movies.run` again at line 99. Lambda function `get_environemnt_from _args`
4. this goes to `environment.movies.configs` at line 291 of `items_loader = MoviesLoader(`
5. This then goes into a bunch of json decoder stuff.

NOTE the file that is is trying to open is named correctly but does not contain JSON but a git commit.  :-/

It's because there is a really really really large file that git pull on its own won't work.  Git lfs pull needs to be done.
