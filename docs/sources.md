# Sources And External Signals

This repository is a public narrative repo. It does not attempt to reproduce
every benchmark from the private engineering repo, but the market thesis is
grounded in visible external signals.

## Low-Bit CPU Inference

- Microsoft BitNet repository:
  <https://github.com/microsoft/BitNet>
- Microsoft Research BitNet CPU inference paper page:
  <https://www.microsoft.com/en-us/research/publication/1-bit-ai-infra-part-1-1-fast-and-lossless-bitnet-b1-58-inference-on-cpus/>
- T-MAC paper:
  <https://arxiv.org/abs/2407.00088>
- T-MAC repository:
  <https://github.com/microsoft/T-MAC>

## ARM Cloud

- AWS Graviton:
  <https://aws.amazon.com/ec2/graviton/>
- AWS Graviton-based SageMaker inference:
  <https://aws.amazon.com/blogs/machine-learning/run-machine-learning-inference-workloads-on-aws-graviton-based-instances-with-amazon-sagemaker/>
- Google Axion:
  <https://cloud.google.com/products/axion>
- Google Compute Engine CPU platforms:
  <https://docs.cloud.google.com/compute/docs/cpu-platforms>
- Google Compute Engine general-purpose machine families:
  <https://cloud.google.com/compute/docs/general-purpose-machines>
- Azure Cobalt:
  <https://azure.microsoft.com/en-us/products/virtual-machines/cobalt>
- Azure Cobalt processor-based VM docs:
  <https://learn.microsoft.com/en-us/azure/virtual-machines/sizes/cobalt-overview>
- Oracle Ampere A1:
  <https://www.oracle.com/cloud/compute/arm/>
- Oracle Always Free resources:
  <https://docs.oracle.com/en-us/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm>
- Arm cloud AI market page:
  <https://www.arm.com/markets/cloud-ai/cloud-computing>

## Device AI / ARM Edge

- Qualcomm AI:
  <https://www.qualcomm.com/products/features/artificial-intelligence>
- Qualcomm Snapdragon 8 Elite Gen 5:
  <https://www.qualcomm.com/smartphones/products/8-series/snapdragon-8-elite-gen-5>
- MediaTek Dimensity AI:
  <https://www.mediatek.com/technology/artificial-intelligence>
- Microsoft Copilot+ PC / Windows ARM ecosystem:
  <https://www.microsoft.com/en-us/windows/copilot-plus-pcs>

## How To Read These Sources

The important external signal is convergence:

1. low-bit models are becoming credible;
2. CPU-first low-bit inference has strong published momentum;
3. ARM cloud is now mainstream;
4. Android and Windows ARM devices are improving quickly;
5. GPU inference remains expensive for small always-on workloads.

`sram_attention` sits at the intersection of those trends.
