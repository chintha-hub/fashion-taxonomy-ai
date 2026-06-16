import streamlit as st
import google.generativeai as genai
from PIL import Image

st.set_page_config(page_title="Fashion Taxonomy AI", page_icon="👗", layout="wide")

st.title("Fashion Taxonomy AI Analyzer")
st.caption("Upload a fashion image to generate a complete taxonomy breakdown")

api_key = st.secrets["GOOGLE_API_KEY"]
genai.configure(api_key=api_key)

PROMPT = """Analyze this fashion image in COMPLETE detail. Provide a structured taxonomy breakdown:

BASIC CLASSIFICATION:
1. CATEGORY: (Tops / Bottoms / Dress / Outerwear / Knitwear / Accessories / Footwear)
2. SUB-CATEGORY: (e.g., Blouse, Midi Dress, Trench Coat)
3. SILHOUETTE: (A-line / Straight / Oversized / Fitted / Relaxed / Wrap / Asymmetric / Boxy)
4. NECKLINE: (V-neck / Round / Square / Off-shoulder / Halter / Collared / Strapless / Cowl)
5. SLEEVE: (Sleeveless / Short / Long / 3/4 / Puff / Rolled / Cape / Draped)
6. LENGTH: (Crop / Short / Midi / Maxi / Mini / Standard / Knee / Ankle)

MATERIAL & COLOR:
7. MATERIAL: (Cotton / Silk / Linen / Denim / Leather / Knit / Chiffon / Satin / Wool / Synthetic)
8. PRIMARY COLOUR: (Name it - Ivory, Navy, Burgundy, etc.)
9. SECONDARY COLOUR: (If applicable)
10. PRINT / TEXTURE: (Solid / Floral / Stripe / Check / Abstract / Geometric / Embroidered / Textured)

DETAILS:
11. KEY DETAIL: (What stands out? - Ruffle, Pocket, Belt, Cut-out, Draping, etc.)
12. FABRIC WEIGHT: (Lightweight / Medium / Heavyweight)
13. FINISH: (Matte / Glossy / Textured)

TREND ANALYSIS:
14. TREND SIGNAL: (Utility femininity / Sheer layering / Tactile surfaces / Oversized tailoring / Quiet luxury / Maximalism / Streetwear / Heritage / Other)
15. TREND CONFIDENCE: (High / Medium / Low / Edge Case)
16. WHY THIS TREND: (Explain in 1-2 sentences)

MARKET POSITIONING:
17. MARKET LEVEL: (Luxury / Premium / Mid-market / Fast-fashion / Accessible)
18. TARGET CUSTOMER: (Who wears this? Age, lifestyle, values)
19. SEASON: (SS26 / AW26 / Timeless)
20. COMPARABLE BRANDS: (Which brands make similar pieces?)

AI ASSESSMENT:
21. CLASSIFICATION DIFFICULTY: (Easy / Medium / Hard / Edge Case)
22. WHY DIFFICULT (if applicable): (What makes this tricky?)
23. AI TRAINING RECOMMENDATION: (How should AI learn from this?)

Be specific and concise."""

uploaded_file = st.file_uploader("Choose a fashion image", type=["jpg", "jpeg", "png"])

if uploaded_file is not None:
    col1, col2 = st.columns([1, 2])

    with col1:
        image = Image.open(uploaded_file)
        st.image(image, caption="Uploaded image", use_container_width=True)

    with col2:
        with st.spinner("Analysing fashion taxonomy..."):
            model = genai.GenerativeModel("gemini-1.5-flash")
            response = model.generate_content([PROMPT, image])
            st.markdown(response.text)
else:
    st.info("Upload an image above to see the taxonomy breakdown.")
