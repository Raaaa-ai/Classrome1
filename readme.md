aloha


# Learning Summary

## 1. Git Basic Workflow and Branch Management
Through this assignment, I have practiced the complete Git version‑control workflow. I learned to clone remote repositories, stage modified files with `git add`, create local snapshots using `git commit`, and upload local commits to a remote repository with `git push`. It is important to understand that `commit` only saves snapshots locally on my machine, and changes will not appear on GitHub until I execute `git push`.

I also learned branch operations. I created a separate feature branch named `for_fun`, which allows me to make changes in an isolated environment without modifying the content on the `main` branch directly. When merging a feature branch back into main, Git may produce merge conflicts if both branches modify the same lines inside one file. Under conflict situations, I need to manually edit the file to resolve conflicting markers before completing the merge commit. Moreover, I can revisit past project states by checking out an old commit hash, entering detached‑HEAD mode to view historical snapshots. This operation inspects history safely and will not destroy my recent commits on the main branch.

## 2. Hugging Face Environment and Pretrained‑Model Inference
I understand that the Hugging Face ecosystem is a collection of Python libraries rather than standalone software. Key packages include `transformers` for pre‑trained models, `datasets` for loading public datasets, together with PyTorch as the deep learning backend. In this task, I loaded ResNet‑50, a convolutional neural network pre‑trained on the large‑scale ImageNet dataset, and ran zero‑shot inference on the MNIST handwritten digit dataset.

Since the ResNet‑50 weights are trained on natural color images from ImageNet and have never seen handwritten digits during training, it only achieves very low accuracy when directly evaluated on MNIST without any fine‑tuning. This demonstrates that pre‑trained models cannot perform well on completely unseen target tasks without further adaptation. During inference, I must switch the model into evaluation mode via `model.eval()` and wrap inference logic inside `torch.no_grad()`. These two settings disable dropout layers and gradient computation, reduce memory overhead and accelerate forward passes.

## 3. Image Preprocessing, Resize and Input Adaptation
Pre‑trained CNN models impose strict requirements for input image shape, resolution and channel count. ResNet‑50 expects 224×224 RGB three‑channel images as network input. However, MNIST dataset provides 28×28 single‑channel grayscale images. Therefore several preprocessing steps are mandatory before feeding data into the model. First, I convert grayscale images into three‑channel RGB format to match channel dimension requirements. Second, I apply an explicit `Resize` transformation to scale small 28×28 images up to the target resolution 224×224. After resizing, the `AutoImageProcessor` handles further operations including normalization and tensor conversion. If image size or channel settings do not satisfy model specifications, inference will produce abnormal outputs.
