### Here I introduce some of my tools to C309 teammates :>

- You can try to see the rebuttal details of the papers released in Openreview.com:
  ```
  https://openreview.net/pdf?id=wT6GHk5ShC. # this is pdf entrence
  https://openreview.net/forum?id=wT6GHk5ShC. # this is rebuttal entrence
  ```
  
- Use this code for downloading pytorch from other sources:
  ```
  pip install torch==2.0.1 -f https://mirrors.aliyun.com/pytorch-wheels/cu118
  ```
- Use this website for helping you to review papers:
  ```
  https://review.cspaper.org/
  ```
- When you use bitsandbytes Pylib in Windows env, you may need to pip install this to build the right file.dll
  
  If your torch version is below torch 2.2.0 and your torch.cuda is like cu118, you can use:
  ```
  pip uninstall bitsandbytes
  pip install https://github.com/jllllll/bitsandbytes-windows-webui/releases/download/wheels/bitsandbytes-0.41.0-py3-none-win_amd64.whl
  ```

  If your torch version is above torch 2.2.0 and your torch.cuda is like cu126, you can just use bitsandbytes, now it's ok for windows:
  ```
  pip install bitsandbytes==0.46.0
  ```

- You can use this website to retrieve and read top conference papers:
  ```
  https://papercopilot.org/
  ```

- This paper use gradient and entropy for finding important tokens for token compression:
  ```
  https://arxiv.org/abs/2505.08392
  ```

- You can use this to get corresponding papers linked to your zotero:
  ```
  https://github.com/TideDra/zotero-arxiv-daily
  ```

- You can use this website for recording your pre-experimental results and switch them to latex table format:
  ```
  https://www.tablesgenerator.com/
  ```

- Your can view you IEEE journal submission in the following links with your scholarone account:
  ```
  https://mc.manuscriptcentral.com/tdsc-cs
  ```

- MIA and defense summary:
  ```
  https://github.com/HongshengHu/membership-inference-machine-learning-literature
  ```
- A nice rebuttal response:
  ```
  https://openreview.net/forum?id=gBgvuTd9Hx
  ```
- You can download various icons or .svg vector for plotting your core alrorithm figure (downloading may require VPN):
  ```
  https://www.flaticon.com/
  ```

- Using Phi-3-Small-128k model may encounter triton error. Please fix it using:
  ```
  https://huggingface.co/microsoft/Phi-3-small-128k-instruct/commit/ed7de9a074b0760e6cf050fe1d103b90834933c8
  ```

  The relevant description is below:
  ```
  https://huggingface.co/microsoft/Phi-3-small-128k-instruct/discussions/19
  ```
  
