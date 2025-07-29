<script>
  import LinkButton from "$lib/components/LinkButton.svelte";
  import Grid from "$lib/components/Grid.svelte";
  import Badge from "$lib/components/Badge.svelte";
  import ProductCard from "$lib/components/ProductCard.svelte";
  import Accordion from "$lib/components/Accordion.svelte";
  import Button from "$lib/components/Button.svelte";

  import DeviceImage from "$lib/images/device.png";
  import BodyImage from "$lib/images/comma-body.png";

  import RecordingsIcon from "$lib/icons/features/recordings.svg?raw";
  import CalendarIcon from "$lib/icons/features/calendar.svg?raw";
  import CurrencyIcon from "$lib/icons/features/currency.svg?raw";
  import BusinessIcon from "$lib/icons/features/business.svg?raw";
  import ContactIcon from "$lib/icons/features/contact.svg?raw";
  import ImmediateIcon from "$lib/icons/features/immediate.svg?raw";
  import AdaptiveCruiseIcon from "$lib/icons/features/adaptive-cruise.svg?raw";
  import LaneCenteringIcon from "$lib/icons/features/lane-centering.svg?raw";

  import { THREEX_PRICE, THREEX_AFFIRM_PRICE, THREEX_SALE, THREEX_STRIKETHROUGH_PRICE } from '$lib/constants/prices.js';
  import { vehicleCountText } from '$lib/constants/vehicles.js';

  import { addToCart } from "../../store";
  import { accessoriesList } from "./productsList";

  $: accessoryProducts = accessoriesList.map((product) => product.productInfo);
</script>

<section class="dark" id="devices">
  <div class="container">
    <article>
      <div class="product-display gradient-bg">
        <div class="aurora"></div>
        <div class="starfield"></div>
        <div class="floating-particles-large"></div>
        <div class="floating-particles-medium"></div>
        <div class="floating-particles-small"></div>
        <div class="dark-overlay"></div>
        <div class="matrix-rain"></div>
        <div class="scan-line"></div>
        <Grid columns={2} alignItems="center" size="large">
          <div class="product-content">
            <Badge style="accent">New low price!</Badge>
            <hgroup>
              <h1>comma 3X</h1>
              <span>
                {#if THREEX_STRIKETHROUGH_PRICE}
                  <span class="strikethrough-price">${THREEX_STRIKETHROUGH_PRICE}</span>
                {/if}
                <span class:sale-price={THREEX_SALE}>${THREEX_PRICE}</span>
              </span>
              <span class="muted">or ${THREEX_AFFIRM_PRICE}/month with Affirm.</span>
            </hgroup>
            <LinkButton href="shop/comma-3x" style="secondary" fullWidth>
              Buy now
            </LinkButton>
            <p>
              Works with {vehicleCountText} cars.
              <a class="highlight muted" href="/vehicles" target="_blank">Check compatibility</a>.
            </p>
          </div>
          <div class="mobile-first">
            <img src={DeviceImage} loading="lazy" alt="comma 3X device" />
          </div>
        </Grid>
      </div>
      <div class="traits light">
        <Grid columns={3} alignItems="stretch" columnGap="0" rowGap="0">
          <div class="trait">
            <div>{@html RecordingsIcon}</div>
            <hgroup>
              <h2>Easy to plug in</h2>
              <div>
                Watch our step-by-step videos. Get set up in your car in 15 minutes.
              </div>
            </hgroup>
          </div>
          <div class="trait">
            <div>{@html CalendarIcon}</div>
            <hgroup>
              <h2>30-day money-back trial</h2>
              <div>
                See for yourself why Consumer Reports rated us as the
                <a class="highlight" href="https://data.consumerreports.org/wp-content/uploads/2020/11/consumer-reports-active-driving-assistance-systems-november-16-2020.pdf" target="_blank">top ADAS system</a>.
              </div>
            </hgroup>
          </div>
          <div class="trait">
            <div>{@html CurrencyIcon}</div>
            <hgroup>
              <h2>Pay over time</h2>
              <div>
                Split your purchase into 3, 6, or 12 monthly payments. On a
                ${THREEX_PRICE} purchase, you may pay ${THREEX_AFFIRM_PRICE} for 12 months with a 15% APR.
              </div>
            </hgroup>
          </div>
        </Grid>
      </div>
    </article>

    <article>
      <div class="product-display">
        <Grid columns={2} alignItems="center" size="large">
          <div class="product-content">
            <Badge style="dark">Robotics Development Kit</Badge>
            <hgroup>
              <h1>body</h1>
              <span>$999</span>
              <span class="muted">or $91/month with Affirm.</span>
            </hgroup>
            <LinkButton href="/shop/body" style="secondary">Buy now</LinkButton>
            <p>
              "the future of people" –
              <a class="highlight muted" href="https://blog.comma.ai/commabody/">Read blog post.</a>
            </p>
          </div>
          <div class="mobile-first">
            <img src={BodyImage} loading="lazy" alt="comma body device" />
          </div>
        </Grid>
      </div>
    </article>
  </div>
</section>

<section class="light" id="accessories">
  <div class="container">
    <hr />
    <h1>Accessories</h1>
    <div class="products-list">
      <Grid columns={3} alignItems="stretch">
        {#each accessoryProducts.slice(0, 6) as product}
          <ProductCard {product} />
        {/each}
      </Grid>
    </div>
    <Accordion style="dark">
      <h2 class="shop-accessories-label" slot="label">Shop all accessories</h2>
      <div class="shop-accessories-list" slot="content">
        <Grid columns={3} alignItems="stretch">
          {#each accessoryProducts.slice(6) as product}
            <ProductCard {product} />
          {/each}
        </Grid>
      </div>
    </Accordion>
  </div>
</section>

<section class="light" id="services">
  <div class="container">
    <hr />
    <h1>Services</h1>
    <div class="service-item">
      <Accordion style="dark">
        <div class="service-label" slot="label">
          <hgroup>
            <h2>Meetings with comma</h2>
            <p>
              Schedule a 30 minute phone call with comma's VP of Business
              Development.
            </p>
            <span>$1000</span>
          </hgroup>
        </div>
        <div class="service-details" slot="content">
          <Grid columns={2}>
            <div>
              <h3>Overview</h3>
              <p>
                Schedule a 30 minute phone call with comma's VP of Business
                Development to discuss potential partnerships, collaborations,
                or questions about the comma ecosystem. For comma related
                inquiries only. Total cost for the meeting is $1000.
              </p>
              <blockquote>
                "The only way you're going to get me for a meeting is if you're
                writing me a check."
              </blockquote>
              <cite>- Mark Cuban</cite>
              <hr />
              <span class="price">$1,000.00</span>
              <Button
                style="accent"
                on:click={() => {
                  addToCart("gid://shopify/ProductVariant/31864968314943");
                }}
              >
                Add to cart
              </Button>
            </div>
            <div>
              <div class="side-by-side">
                {@html BusinessIcon}
                <hgroup>
                  <h4>Partnerships</h4>
                  <p>
                    Pitch ideas for potential collaboration with comma and our
                    ecosystem.
                  </p>
                </hgroup>
              </div>
              <hr />
              <div class="side-by-side">
                {@html ContactIcon}
                <hgroup>
                  <h4>Inquiries</h4>
                  <p>
                    Get a better understanding of comma services, products, and
                    limitations.
                  </p>
                </hgroup>
              </div>
              <hr />
              <div class="side-by-side">
                {@html ImmediateIcon}
                <hgroup>
                  <h4>Prompt Scheduling</h4>
                  <p>
                    Order today and get a response in days for immediate
                    scheduling.
                  </p>
                </hgroup>
              </div>
            </div>
          </Grid>
        </div>
      </Accordion>
    </div>

    <div class="service-item">
      <Accordion style="dark">
        <div class="service-label" slot="label">
          <hgroup>
            <h2>Custom car ports</h2>
            <p>
              Hire the openpilot team to add support for additional car brands
              and models.
            </p>
            <span>See pricing</span>
          </hgroup>
        </div>
        <div class="service-details" slot="content">
          <Grid columns={2}>
            <div>
              <h3>Overview</h3>
              <p>
                comma openpilot is an open source driver-assistance system.
                Currently, openpilot performs the functions of Adaptive Cruise
                Control (ACC) and Automated Lane Centering (ALC) and Lane Change
                Assist for <a class="highlight" href="/vehicles" tabindex="0">compatible vehicles</a>.
                It performs similarly to Tesla Autopilot and GM Super Cruise.
                openpilot can steer, accelerate, and brake automatically for other vehicles within its lane.
              </p>
              <p>
                Hire the comma openpilot team to add dedicated support for a new
                make or model vehicle that has electronically controllable gas,
                brake, and steering. We will work until the port is upstreamed,
                or on a branch for non production cars.<br />
              </p>
              <p>
                A car must be provided to comma prior to beginning the project.
                The porting fee includes an installed working comma 3X when the
                car is returned and open sourcing of the required interface
                hardware.<br />
              </p>
              <p>
                This service is intended for pre/non production vehicles. For
                production vehicles on the market today, we will likely do the
                port much cheaper, perhaps as cheap as the cost of the car.
              </p>
              <strong>Included</strong>
              <ul>
                <li>Fully working port for openpilot</li>
                <li>comma 3X installed in returned car</li>
                <li>Completed in 12 weeks</li>
              </ul>
              <strong>Pricing</strong>
              <ul>
                <li>$50,000 Down Payment (immediate)</li>
                <li>$500,000 Total (due at start of project)</li>
              </ul>
              <hr />
              <span class="price">$50,000.00</span>
              <Button
                style="accent"
                on:click={() => {
                  addToCart("gid://shopify/ProductVariant/31864934662207");
                }}
              >
                Add to cart
              </Button>
            </div>
            <div>
              <div class="side-by-side">
                {@html AdaptiveCruiseIcon}
                <hgroup>
                  <h4>Adaptive Cruise</h4>
                  <p>
                    Adjusts speed to maintain a safe distance from vehicles
                    ahead.
                  </p>
                </hgroup>
              </div>
              <hr />
              <div class="side-by-side">
                {@html LaneCenteringIcon}
                <hgroup>
                  <h4>Auto Lane Centering</h4>
                  <p>
                    Steers and brakes to continually center the vehicle in its
                    lane.
                  </p>
                </hgroup>
              </div>
              <hr />
              <div class="side-by-side">
                {@html ImmediateIcon}
                <hgroup>
                  <h4>Completed in 12 Weeks</h4>
                  <p>Get the fully working port for openpilot upstreamed.</p>
                </hgroup>
              </div>
            </div>
          </Grid>
        </div>
      </Accordion>
    </div>
  </div>
</section>

<style>
  section {
    background-color: unset;
  }

  #devices {
    padding: 4rem 0 0;

    & article {
      border: 1px solid #000;

      &:first-of-type {
        margin-bottom: 4rem;
      }
    }

    & .gradient-bg {
      --overlay-darkness: 0.6; /* Tweak this value: 0 = no overlay, 1 = full black */
      
      position: relative;
      background: 
        /* Deep matrix portal depth */
        radial-gradient(circle at center, rgba(0, 0, 0, 0.1) 15%, rgba(0, 0, 0, 0.5) 40%, rgba(0, 0, 0, 0.8) 70%),
        /* Matrix green energy zones with depth */
        radial-gradient(circle at 20% 80%, rgba(0, 255, 0, 0.3) 0%, rgba(0, 255, 0, 0.1) 30%, transparent 50%),
        radial-gradient(circle at 80% 20%, rgba(0, 255, 127, 0.25) 0%, rgba(0, 255, 127, 0.08) 35%, transparent 55%),
        radial-gradient(ellipse at 50% 50%, rgba(0, 255, 0, 0.15) 0%, rgba(0, 255, 0, 0.05) 40%, transparent 70%),
        /* Subtle orange accent pops */
        radial-gradient(circle at 70% 30%, rgba(255, 140, 0, 0.12) 0%, transparent 25%),
        radial-gradient(circle at 30% 70%, rgba(255, 165, 0, 0.08) 0%, transparent 30%),
        /* Additional depth layers */
        radial-gradient(circle at 40% 20%, rgba(0, 255, 0, 0.1) 0%, transparent 40%),
        radial-gradient(circle at 60% 80%, rgba(0, 255, 127, 0.08) 0%, transparent 35%),
        /* Deep matrix background */
        linear-gradient(135deg, #000000 0%, #001100 25%, #000a00 50%, #001100 75%, #000000 100%);
      overflow: hidden;
      box-shadow: 
        inset 0 0 300px rgba(0, 0, 0, 0.9),
        inset 0 0 150px rgba(0, 255, 0, 0.15),
        inset 0 0 80px rgba(255, 140, 0, 0.08),
        inset 0 0 40px rgba(0, 255, 127, 0.1);
      
      /* Subtle matrix aurora effect */
      & > .aurora {
        position: absolute;
        inset: 0;
        background: 
          linear-gradient(35deg, 
            transparent 20%, 
            rgba(0, 255, 0, 0.08) 30%, 
            rgba(0, 255, 127, 0.12) 45%, 
            rgba(255, 140, 0, 0.06) 55%, 
            rgba(0, 255, 0, 0.08) 70%, 
            transparent 80%
          );
        filter: blur(60px);
        transform: skewY(-3deg) scale(2);
        animation: aurora 40s ease-in-out infinite alternate;
        pointer-events: none;
        opacity: 0.6;
      }
      
      @keyframes aurora {
        0% { transform: skewY(-5deg) scale(1.5) translateX(-10%); }
        100% { transform: skewY(5deg) scale(1.5) translateX(10%); }
      }
      
      /* Subtle matrix starfield */
      & > .starfield {
        position: absolute;
        inset: 0;
        background-image: 
          radial-gradient(1px 1px at 20px 30px, rgba(255, 255, 255, 0.6), transparent),
          radial-gradient(1px 1px at 40px 70px, rgba(255, 255, 255, 0.4), transparent),
          radial-gradient(0.5px 0.5px at 50px 160px, rgba(255, 255, 255, 0.5), transparent),
          radial-gradient(1px 1px at 130px 40px, rgba(255, 255, 255, 0.3), transparent),
          radial-gradient(1px 1px at 80px 120px, rgba(0, 255, 0, 0.4), transparent),
          radial-gradient(0.5px 0.5px at 110px 90px, rgba(255, 255, 255, 0.4), transparent),
          radial-gradient(0.5px 0.5px at 160px 20px, rgba(255, 255, 255, 0.3), transparent),
          radial-gradient(1px 1px at 180px 140px, rgba(255, 140, 0, 0.3), transparent),
          radial-gradient(0.5px 0.5px at 90px 180px, rgba(0, 255, 127, 0.3), transparent);
        background-size: 200px 200px;
        animation: sparkle 60s linear infinite;
        pointer-events: none;
        opacity: 0.7;
      }
      
      @keyframes sparkle {
        0% { opacity: 0.5; transform: rotate(0deg) scale(1); }
        50% { opacity: 1; }
        100% { opacity: 0.5; transform: rotate(360deg) scale(1); }
      }
      
      /* Large floating circle particles */
      & > .floating-particles-large {
        position: absolute;
        inset: 0;
        background-image:
          /* Large matrix green circles */
          radial-gradient(circle at 25% 120%, rgba(0, 255, 0, 0.6) 0%, rgba(0, 255, 0, 0.3) 20%, rgba(0, 255, 0, 0.1) 40%, transparent 50%),
          radial-gradient(circle at 65% 115%, rgba(0, 255, 127, 0.5) 0%, rgba(0, 255, 127, 0.25) 25%, rgba(0, 255, 127, 0.08) 45%, transparent 55%),
          radial-gradient(circle at 85% 125%, rgba(0, 255, 0, 0.4) 0%, rgba(0, 255, 0, 0.2) 30%, rgba(0, 255, 0, 0.06) 50%, transparent 60%),
          /* Subtle orange accent circles */
          radial-gradient(circle at 45% 130%, rgba(255, 140, 0, 0.3) 0%, rgba(255, 140, 0, 0.15) 25%, rgba(255, 140, 0, 0.05) 45%, transparent 55%);
        background-size: 100% 100%;
        filter: blur(8px);
        animation: floatLarge 35s linear infinite;
        pointer-events: none;
        z-index: 1;
      }
      
      @keyframes floatLarge {
        0% { 
          opacity: 0;
        }
        15% { opacity: 1; }
        85% { opacity: 1; }
        100% { 
          opacity: 0;
        }
      }
      
      /* Medium floating circle particles */
      & > .floating-particles-medium {
        position: absolute;
        inset: 0;
        background-image:
          /* Medium matrix green circles */
          radial-gradient(circle at 20% 125%, rgba(0, 255, 0, 0.7) 0%, rgba(0, 255, 0, 0.4) 15%, rgba(0, 255, 0, 0.1) 35%, transparent 45%),
          radial-gradient(circle at 40% 120%, rgba(0, 255, 127, 0.6) 0%, rgba(0, 255, 127, 0.3) 20%, rgba(0, 255, 127, 0.08) 40%, transparent 50%),
          radial-gradient(circle at 60% 135%, rgba(0, 255, 0, 0.5) 0%, rgba(0, 255, 0, 0.25) 25%, rgba(0, 255, 0, 0.06) 45%, transparent 55%),
          radial-gradient(circle at 80% 115%, rgba(0, 255, 127, 0.6) 0%, rgba(0, 255, 127, 0.3) 18%, rgba(0, 255, 127, 0.08) 38%, transparent 48%),
          /* Occasional orange accent */
          radial-gradient(circle at 70% 128%, rgba(255, 140, 0, 0.4) 0%, rgba(255, 140, 0, 0.2) 20%, rgba(255, 140, 0, 0.05) 40%, transparent 50%);
        background-size: 100% 100%;
        filter: blur(4px);
        animation: floatMedium 25s linear infinite;
        animation-delay: 8s;
        pointer-events: none;
        z-index: 1;
      }
      
      @keyframes floatMedium {
        0% { 
          transform: perspective(800px) translateZ(-100px) translateY(0) translateX(0) scale(0.5);
          opacity: 0;
        }
        12% { opacity: 1; }
        88% { opacity: 1; }
        100% { 
          opacity: 0;
        }
      }
      
      /* Small floating circle particles */
      & > .floating-particles-small {
        position: absolute;
        inset: 0;
        background-image:
          /* Small matrix green circles */
          radial-gradient(circle at 15% 118%, rgba(0, 255, 0, 0.8) 0%, rgba(0, 255, 0, 0.5) 10%, rgba(0, 255, 0, 0.15) 25%, transparent 35%),
          radial-gradient(circle at 35% 125%, rgba(0, 255, 127, 0.7) 0%, rgba(0, 255, 127, 0.4) 12%, rgba(0, 255, 127, 0.12) 28%, transparent 38%),
          radial-gradient(circle at 55% 132%, rgba(0, 255, 0, 0.6) 0%, rgba(0, 255, 0, 0.35) 15%, rgba(0, 255, 0, 0.1) 30%, transparent 40%),
          radial-gradient(circle at 75% 120%, rgba(0, 255, 127, 0.7) 0%, rgba(0, 255, 127, 0.4) 10%, rgba(0, 255, 127, 0.12) 25%, transparent 35%),
          radial-gradient(circle at 95% 115%, rgba(0, 255, 0, 0.5) 0%, rgba(0, 255, 0, 0.3) 15%, rgba(0, 255, 0, 0.08) 30%, transparent 40%),
          radial-gradient(circle at 45% 140%, rgba(0, 255, 127, 0.6) 0%, rgba(0, 255, 127, 0.35) 12%, rgba(0, 255, 127, 0.1) 28%, transparent 38%),
          /* Rare small orange accent */
          radial-gradient(circle at 65% 127%, rgba(255, 140, 0, 0.4) 0%, rgba(255, 140, 0, 0.2) 15%, rgba(255, 140, 0, 0.05) 30%, transparent 40%);
        background-size: 100% 100%;
        filter: blur(2px);
        animation: floatSmall 18s linear infinite;
        animation-delay: 15s;
        pointer-events: none;
        z-index: 2;
      }
      
      @keyframes floatSmall {
        0% { 
          opacity: 0;
        }
        8% { opacity: 1; }
        92% { opacity: 1; }
        100% { 
          opacity: 0;
        }
      }
      
      /* Grain effect using pseudo-element */
      &::before {
        content: "";
        position: absolute;
        inset: 0;
        background-image: 
          repeating-conic-gradient(
            from 0deg at 50% 50%,
            rgba(0, 255, 0, 0.08) 0deg,
            transparent 1deg,
            transparent 2deg,
            rgba(255, 140, 0, 0.08) 3deg,
            transparent 4deg,
            transparent 5deg,
            rgba(0, 255, 127, 0.07) 6deg
          );
        opacity: 1;
        mix-blend-mode: screen;
        pointer-events: none;
        animation: grain 15s infinite linear;
      }
      
      @keyframes grain {
        0%, 100% { transform: translate(0, 0) scale(1); }
        25% { transform: translate(-5%, 5%) scale(1.05); }
        50% { transform: translate(5%, -5%) scale(0.95); }
        75% { transform: translate(-5%, -5%) scale(1.02); }
      }
      
      /* Grainy noise texture */
      &::after {
        content: "";
        position: absolute;
        inset: 0;
        opacity: 0.5;
        mix-blend-mode: screen;
        background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='300' height='300'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='turbulence' baseFrequency='0.95' numOctaves='4' stitchTiles='stitch'/%3E%3CfeColorMatrix type='saturate' values='0'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)' opacity='1'/%3E%3C/svg%3E");
        pointer-events: none;
      }
      
      /* Dark overlay for easy brightness control */
      & > .dark-overlay {
        position: absolute;
        inset: 0;
        background-color: rgba(0, 0, 0, var(--overlay-darkness));
        pointer-events: none;
        z-index: 1;
      }
      
      /* Matrix rain effect */
      & > .matrix-rain {
        position: absolute;
        inset: 0;
        background-image: 
          repeating-linear-gradient(
            90deg,
            transparent 0,
            transparent 18px,
            rgba(0, 255, 0, 0.04) 18px,
            rgba(0, 255, 0, 0.04) 19px,
            transparent 19px,
            transparent 36px,
            rgba(255, 140, 0, 0.02) 36px,
            rgba(255, 140, 0, 0.02) 37px,
            transparent 37px,
            transparent 54px,
            rgba(0, 255, 127, 0.03) 54px,
            rgba(0, 255, 127, 0.03) 55px,
            transparent 55px,
            transparent 72px,
            rgba(255, 165, 0, 0.015) 72px,
            rgba(255, 165, 0, 0.015) 73px,
            transparent 73px,
            transparent 90px
          );
        animation: matrixRain 30s linear infinite;
        pointer-events: none;
        z-index: 1;
      }
      
      @keyframes matrixRain {
        0% { transform: translateY(0); }
        100% { transform: translateY(100px); }
      }
      
      /* Ensure content stays above pseudo-elements */
      & > * {
        position: relative;
        z-index: 2;
      }
      
      /* Animated scan line for extra retro effect */
      & > .scan-line {
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        height: 4px;
        background: linear-gradient(90deg, 
          transparent 0%, 
          rgba(255, 140, 0, 0.7) 10%,
          rgba(0, 255, 0, 0.9) 25%,
          rgba(0, 255, 127, 0.9) 40%,
          rgba(255, 165, 0, 0.8) 50%,
          rgba(0, 255, 127, 0.9) 60%,
          rgba(0, 255, 0, 0.9) 75%,
          rgba(255, 94, 77, 0.6) 90%,
          transparent 100%
        );
        filter: blur(1px);
        opacity: 0.8;
        animation: scan 10s linear infinite;
        pointer-events: none;
        mix-blend-mode: screen;
        z-index: 2;
      }
    }
    
    @keyframes scan {
      0% { transform: translateY(0); }
      100% { transform: translateY(100vh); }
    }
    
    /* Subtle flicker animation for space effect */
    & .gradient-bg {
      animation: spaceFlicker 45s infinite;
    }
    
    @keyframes spaceFlicker {
      0%, 100% { filter: brightness(1) saturate(1); }
      25% { filter: brightness(1.05) saturate(1.1); }
      50% { filter: brightness(0.98) saturate(1); }
      75% { filter: brightness(1.02) saturate(1.05); }
      92% { filter: brightness(1); }
      92.5% { filter: brightness(1.08) hue-rotate(10deg); }
      93% { filter: brightness(0.97); }
      93.5% { filter: brightness(1); }
    }

    & .product-display {
      padding: 6rem;
      background-color: black;

      & hgroup {
        margin-bottom: 2rem;

        & h1 {
          font-size: 2.5rem;
        }

        & span {
          display: block;

          &:first-of-type {
            font-size: 1.5rem;
          }
        }

        & .strikethrough-price {
          text-decoration: line-through;
        }

        & .sale-price {
          font-weight: 700;
          color: var(--color-red);
        }

      }

      & p {
        font-size: 1.125rem;
        color: white;
      }

      & .muted {
        color: white;
        opacity: 0.75;
      }
    }

    & .traits {
      align-items: stretch;

      & .trait {
        display: flex;
        align-content: flex-start;
        padding: 1.5rem;

        & svg {
          margin-right: 1rem;
        }

        & h2 {
          font-size: 1rem;
          font-weight: 600;
          text-transform: uppercase;
          margin-bottom: 0.5rem;
        }

        border-right: 1px solid #000;

        &:last-of-type {
          border-right: none;
        }
      }
    }

    @media only screen and (max-width: 1024px) {
      & {
        padding: 2.5rem 0 0;
      }


      & .product-display {
        padding: 2rem;
        text-align: center;

        & .product-content {
          display: flex;
          flex-direction: column;
          align-items: center;

          & > a {
            width: 100%;
            box-sizing: border-box;
          }
        }
      }

      & .trait {
        flex-wrap: wrap;

        & svg {
          margin-right: 0;
          margin-bottom: 1rem;
        }
      }
    }

    @media only screen and (max-width: 768px) {
      & .trait {
        flex-wrap: nowrap;

        border-right: none !important;
        border-bottom: 1px solid #000;
      }

      & .trait:last-of-type {
        border-bottom: none;
      }
    }
  }

  section .container > hr {
    margin-top: 0rem;
    margin-bottom: 2rem;

    & + h1 {
      margin-bottom: 3rem;
    }
  }

  .products-list {
    margin: 2rem 0;
  }

  #accessories {
    & .shop-accessories-label {
      text-align: center;
      padding: 2rem 0;
      margin-bottom: 0;
      font-size: 1.25rem;
      font-weight: 600;
    }

    & .shop-accessories-list {
      margin-top: 2rem;
    }
  }

  .service-item {
    margin-bottom: 3rem;

    & .service-label {
      color: white;
      background-color: black;
      padding: 2rem;

      & hgroup {
        & * {
          color: white;
          line-height: 1.25;
        }

        & h2 {
          margin-bottom: 0.25rem;
          font-size: 1.75rem;
          font-weight: 600;
        }

        & p {
          opacity: 0.65;
          font-size: 1.25rem;
          margin-top: 0;
        }

        & span {
          margin-top: 0.875rem;
          font-size: 1.25rem;
        }
      }
      color: white;
      font-size: 1.5rem;
      font-weight: 600;
    }

    & .service-details {
      border: 1px solid #000;
      padding: 3rem 2rem;
      color: black;

      & h3 {
        margin-top: 0;
      }

      & span {
        font-weight: 700;
      }

      & hr {
        margin: 1.5rem 0;
      }

      & .side-by-side {
        display: flex;
        align-items: center;
        color: black;

        & hgroup {
          margin-left: 1rem;

          & * {
            margin: 0;
          }
          & h4 {
            font-weight: 600;
          }
        }
      }

      & .price {
        display: block;
        margin-bottom: 1rem;
        color: #4a4a4a;
      }
    }
  }
</style>
