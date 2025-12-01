import streamlit as st
import math

st.set_page_config(page_title="Scientific Calculator", page_icon="🧮")

st.title("Scientific Calculator 🧮")
st.write("Perform basic and scientific calculations.")

# --- Mode selection ---
mode = st.radio(
    "Choose mode",
    ["Basic", "Scientific"]
)

st.write("----")

# --- BASIC MODE ---
if mode == "Basic":
    st.subheader("Basic Operations")

    num1 = st.number_input("First number", value=0.0, key="b_num1")
    num2 = st.number_input("Second number", value=0.0, key="b_num2")

    operation = st.selectbox(
        "Operation",
        ["Add (+)", "Subtract (-)", "Multiply (×)", "Divide (÷)"],
        key="b_op"
    )

    if st.button("Calculate (Basic)"):
        if operation == "Add (+)":
            result = num1 + num2
            st.success(f"{num1} + {num2} = {result}")
        elif operation == "Subtract (-)":
            result = num1 - num2
            st.success(f"{num1} - {num2} = {result}")
        elif operation == "Multiply (×)":
            result = num1 * num2
            st.success(f"{num1} × {num2} = {result}")
        elif operation == "Divide (÷)":
            if num2 == 0:
                st.error("❌ Cannot divide by zero.")
            else:
                result = num1 / num2
                st.success(f"{num1} ÷ {num2} = {result}")

# --- SCIENTIFIC MODE ---
else:
    st.subheader("Scientific Operations")

    # Tabs for organization
    tab1, tab2, tab3, tab4 = st.tabs(["Unary (1 number)", "Binary (2 numbers)", "Angle & Trig", "Expression"])

    # --- TAB 1: Unary operations (one number) ---
    with tab1:
        x = st.number_input("Enter a number (x)", value=0.0, key="s_unary_x")
        unary_op = st.selectbox(
            "Choose operation",
            [
                "Square (x²)",
                "Cube (x³)",
                "Square root (√x)",
                "Cube root (∛x)",
                "Absolute value (|x|)",
                "Natural log (ln x)",
                "Log base 10 (log₁₀ x)",
                "Exponential (eˣ)",
                "Factorial (x!) - integer only"
            ],
            key="s_unary_op"
        )

        if st.button("Calculate (Unary)"):
            try:
                if unary_op == "Square (x²)":
                    res = x ** 2
                elif unary_op == "Cube (x³)":
                    res = x ** 3
                elif unary_op == "Square root (√x)":
                    if x < 0:
                        st.error("❌ Cannot take square root of negative number (real domain).")
                        res = None
                    else:
                        res = math.sqrt(x)
                elif unary_op == "Cube root (∛x)":
                    # cube root works for negative numbers too
                    res = math.copysign(abs(x) ** (1/3), x)
                elif unary_op == "Absolute value (|x|)":
                    res = abs(x)
                elif unary_op == "Natural log (ln x)":
                    if x <= 0:
                        st.error("❌ ln(x) defined only for x > 0.")
                        res = None
                    else:
                        res = math.log(x)
                elif unary_op == "Log base 10 (log₁₀ x)":
                    if x <= 0:
                        st.error("❌ log₁₀(x) defined only for x > 0.")
                        res = None
                    else:
                        res = math.log10(x)
                elif unary_op == "Exponential (eˣ)":
                    res = math.exp(x)
                elif unary_op == "Factorial (x!) - integer only":
                    if x < 0 or int(x) != x:
                        st.error("❌ Factorial is only defined for non-negative integers.")
                        res = None
                    else:
                        res = math.factorial(int(x))

                if res is not None:
                    st.success(f"Result = {res}")
            except OverflowError:
                st.error("❌ Result is too large.")

    # --- TAB 2: Binary operations (two numbers) ---
    with tab2:
        a = st.number_input("First number (a)", value=0.0, key="s_bin_a")
        b = st.number_input("Second number (b)", value=0.0, key="s_bin_b")
        bin_op = st.selectbox(
            "Choose operation",
            [
                "Add (a + b)",
                "Subtract (a - b)",
                "Multiply (a × b)",
                "Divide (a ÷ b)",
                "Power (a^b)",
                "Modulo (a % b)"
            ],
            key="s_bin_op"
        )

        if st.button("Calculate (Binary)"):
            if bin_op == "Add (a + b)":
                res = a + b
            elif bin_op == "Subtract (a - b)":
                res = a - b
            elif bin_op == "Multiply (a × b)":
                res = a * b
            elif bin_op == "Divide (a ÷ b)":
                if b == 0:
                    st.error("❌ Cannot divide by zero.")
                    res = None
                else:
                    res = a / b
            elif bin_op == "Power (a^b)":
                try:
                    res = a ** b
                except OverflowError:
                    st.error("❌ Result is too large.")
                    res = None
            elif bin_op == "Modulo (a % b)":
                if b == 0:
                    st.error("❌ Cannot take modulo by zero.")
                    res = None
                else:
                    res = a % b

            if res is not None:
                st.success(f"Result = {res}")

    # --- TAB 3: Angle & Trigonometric functions ---
    with tab3:
        angle_unit = st.radio("Angle unit", ["Degrees", "Radians"], key="s_angle_unit")

        angle_value = st.number_input("Angle value", value=0.0, key="s_angle_value")

        trig_op = st.selectbox(
            "Trigonometric function",
            ["sin", "cos", "tan", "arcsin", "arccos", "arctan"],
            key="s_trig_op"
        )

        if st.button("Calculate (Trig)"):
            # convert to radians if needed
            if angle_unit == "Degrees" and trig_op in ["sin", "cos", "tan"]:
                x_rad = math.radians(angle_value)
            else:
                x_rad = angle_value

            try:
                if trig_op == "sin":
                    res = math.sin(x_rad)
                elif trig_op == "cos":
                    res = math.cos(x_rad)
                elif trig_op == "tan":
                    res = math.tan(x_rad)
                elif trig_op == "arcsin":
                    if angle_value < -1 or angle_value > 1:
                        st.error("❌ arcsin(x) defined only for -1 ≤ x ≤ 1.")
                        res = None
                    else:
                        res = math.asin(angle_value)
                        if angle_unit == "Degrees":
                            res = math.degrees(res)
                elif trig_op == "arccos":
                    if angle_value < -1 or angle_value > 1:
                        st.error("❌ arccos(x) defined only for -1 ≤ x ≤ 1.")
                        res = None
                    else:
                        res = math.acos(angle_value)
                        if angle_unit == "Degrees":
                            res = math.degrees(res)
                elif trig_op == "arctan":
                    res = math.atan(angle_value)
                    if angle_unit == "Degrees":
                        res = math.degrees(res)

                if res is not None:
                    st.success(f"Result = {res}")
            except Exception as e:
                st.error(f"❌ Error: {e}")

    # --- TAB 4: Free expression evaluation ---
    with tab4:
        st.write("Write a mathematical expression using Python syntax, e.g.:")
        st.code("2*3 + math.sin(math.radians(30))")

        expr = st.text_input("Expression", value="2+3*4", key="s_expr")

        if st.button("Evaluate Expression"):
            try:
                # VERY restricted eval environment
                allowed_names = {
                    k: v for k, v in math.__dict__.items()
                    if not k.startswith("__")
                }
                allowed_names["abs"] = abs
                allowed_names["round"] = round

                result = eval(expr, {"__builtins__": {}}, allowed_names)
                st.success(f"Result = {result}")
            except Exception as e:
                st.error(f"❌ Invalid expression: {e}")

st.write("---")
st.caption("Scientific Calculator built with Streamlit")
