<!--
    @component
    A call-to-action component that attracts attention and encourages user engagement.

    Usage:
    ```html
    <CallToAction
      title="Get started today"
      subtitle="Join now"
      description="Ready to experience the difference? Join our community of satisfied customers and see how our solution can transform your workflow."
      image="https://www.unc.mn/image-placeholder.svg"
      callsToAction={[
        {
          href: "/get-started",
          label: "Get Started",
          variant: "primary"
        },
        {
          href: "/contact",
          label: "Talk to Sales",
          variant: "secondary"
        }
      ]}
    />
    ```

    Props:
    - `title`: The main heading text (string)
    - `subtitle`: Secondary heading text (string)
    - `description`: Detailed information about the offer (string)
    - `callsToAction`: Array of CTA objects with href, label, and optional variant properties (CTA[])
    - `imageSrc`: portrait of the company's customer smiling at the camera.
-->

<script lang="ts">
	// Types
	import type { ComponentProps } from "svelte";

	// Components
	import Button from "../ui/Button.svelte";
	import AnimateText from "../animation/AnimateText.svelte";
	import { cta } from "$lib/navigation";

	// Types
	type CTA = {
		href: string;
		label: string;
		variant?: ComponentProps<typeof Button>["variant"];
	};

	// Props
	const {
		title = "Get started today",
		subtitle = "Join now",
		description = "Ready to experience the difference? Join our community of satisfied customers and see how our solution can transform your workflow. ",
		imageSrc = "https://www.unc.mn/image-placeholder.svg",
		callsToAction = [cta],
		...rest
	}: {
		title?: string;
		subtitle?: string;
		description?: string;
		imageSrc?: string;
		callsToAction?: CTA[];
		[key: string]: any;
	} = $props();
</script>

<div class="" {...rest}>
	<section class="section-px section-py container mx-auto">
		<div
			class="bg-card border-border grid content-start items-center justify-between gap-8 rounded-[var(--radius-xl)] border p-8 text-balance shadow-sm transition-all duration-300 hover:shadow-md lg:grid-cols-[2fr_1fr] lg:gap-12"
		>
			<div class="grid h-full content-between gap-8">
				<h2 class="text-title1 mb-2 flex flex-col">
					<span class="font-semibold"><AnimateText text={title} /></span>
					<span class="text-emphasis-low font-normal"><AnimateText text={subtitle} /></span>
				</h2>
				<div class="flex flex-col items-start justify-start gap-6">
					<p class="text-headline text-emphasis-low leading-relaxed">
						{description}
					</p>
					<div class="flex w-full flex-col gap-3 md:flex-row md:flex-wrap md:gap-4">
						{#each callsToAction as cta, index}
							<Button 
								class={[
									"w-full md:w-auto transition-transform duration-200 hover:scale-105 active:scale-95",
									index === 0 ? "shadow-md hover:shadow-lg" : ""
								]}
								href={cta.href} 
								variant={cta.variant || "primary"}
								size="lg"
							>
								{cta.label}
							</Button>
						{/each}
					</div>
				</div>
			</div>
			<div class="relative hidden lg:block">
				<div class="absolute inset-0 bg-gradient-to-br from-primary-50 to-primary-100 rounded-[var(--radius-lg)] opacity-20 blur-xl"></div>
				<img
					src={imageSrc}
					alt="Professional roofing contractor achieving success"
					class="relative aspect-[4/5] size-full max-h-full w-full rounded-[var(--radius-lg)] object-cover transition-transform duration-300 hover:scale-105"
				/>
			</div>
		</div>
	</section>
</div>
