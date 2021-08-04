<script>
const DELAY_MODIFICATOR = 30;

export default {
	name: "ListRender",
	functional: true,
	props: {
		class: {
			type: String,
			default: "list"
		},
		tag: {
			type: String,
			default: "div"
		},
		animation: {
			type: String,
			default: "list-item-fade"
		},
		step: {
			type: [Number, String],
			default: 10
		}
	},
  render(createElement, { props, children, data })
  {
		function setAnimation(el, id) {
			el.data.staticStyle = {
				animationDelay: id * DELAY_MODIFICATOR + "ms"
			};
			el.data.staticClass = el?.data?.staticClass ? `${el.data.staticClass} ${props.animation}` : props.animation;
		}
		let items = children;
		if(children.length > +props.step) items = children.filter((el, id) => id > children.length - Number(props.step) - 1 );
		items.forEach((child, index) => {
			setAnimation(child, index);
		});
    return createElement(props.tag, { class: data.staticClass }, children);
  }
}
</script>

<style scoped>
@keyframes list-item-fade {
	from {
		opacity: 0;
		transform: translateY(4px);
	}
	to {
		opacity: 1;
		transform: translateY(0);
	}
}

::v-deep .list-item-fade {
	opacity: 0;
	transform: translateY(4px);
	animation: list-item-fade 250ms ease-in-out forwards;
}
</style>